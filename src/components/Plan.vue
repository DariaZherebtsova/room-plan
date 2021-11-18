<template>
  <div v-if="!isLoading" class="plan">
    <PlanSVG ref="svg" @click="onClickPlan" />
    <TableSVG
      v-show="false"
      ref="table"
    />
  </div>
</template>

<script>
import * as d3 from 'd3';
import PlanSVG from '@/assets/images/plan.svg';
import TableSVG from '@/assets/images/table.svg';
import tables from "@/assets/data/tables.json";
import legend from "@/assets/data/legend.json";

export default {
  components: {
    PlanSVG,
    TableSVG,
  },
  data() {
    return {
      isLoading: false,
      planSVG: null,
      planSVGgroup: null,
      tableSVG: null,
      tables: [],
    };
  },
  created() {
    this.tables = tables;
  },
  mounted() {
    this.isLoading = true;

    this.planSVG = d3.select(this.$refs.svg);
    this.planSVGgroup = this.planSVG.select("g");
    this.tableSVG = d3.select(this.$refs.table);
    if (this.planSVGgroup) {
      this.drawTables();
    } else {
      console.error("SVG is incorrect");
    }
    
    this.isLoading = false;
  },
  methods: {
    drawTables() {
      const svgTablesGroupPlace = this.planSVGgroup
        .append("g")
        .classed("groupPlaces", true); 

      this.tables.map((table) => {
        const targetSeat = svgTablesGroupPlace
          .append("g")
          .attr("transform", `translate(${table.x}, ${table.y}) scale(0.3)`)
          .attr("id", table._id)
          .classed("employer-place", true);

        targetSeat
          .append("g")
          .attr("transform", `rotate(${table.rotate || 0})`)
          .attr("group_id", table.group_id)
          .classed("table", true)
          .html(this.tableSVG.html())
          .attr(
            "fill",
            legend.find((it) => it.group_id === table.group_id) 
                ?.color ?? "transparent"
          );
      });
    },
  onClickPlan(event) {
      const table = event.target.closest(".employer-place");

      if (table) {
        console.log('place id', table.id);
      }
    },
  }

}
</script>

<style>
.plan {
  display: flex;
  justify-content: center;
}
</style>
