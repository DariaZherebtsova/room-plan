<template>
  <div class="plan">
    <PlanSVG ref="svg" />
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
      svg: null,
      g: null,
      tableSVG: null,
      tables: [],
    };
  },
  created() {
    this.tables = tables;
  },
  mounted() {
    this.isLoading = true;

    this.svg = d3.select(this.$refs.svg);
    this.g = this.svg.select("g");
    this.tableSVG = d3.select(this.$refs.table);
    if (this.g) {
      this.drawTables();
    } else {
      alert("SVG is incorrect");
    }
    
    this.isLoading = false;
  },
  methods: {
    drawTables() {
      console.log('---drawTables');
     // создаем группу для рабочих мест

      const svgTablesGroupPlace = this.g
        .append("g")
        .classed("groupPlaces", true); 

      this.tables.map((table) => {
        // создает группу для рабочего стола
        const targetSeat = svgTablesGroupPlace
          .append("g")
          .attr("transform", `translate(${table.x}, ${table.y}) scale(0.3)`)
          .attr("id", table._id)
          .classed("employer-place", true);

        // устанавливает стол в группу
        targetSeat
          .append("g")
          .attr("transform", `rotate(${table.rotate || 0})`)
          .attr("group_id", table.group_id)
          .classed("table", true)
          .html(this.tableSVG.html())
          .attr( // устанавливаем цвет подразделения
            "fill",
            legend.find((it) => it.group_id === table.group_id) 
                ?.color ?? "transparent"
    );  

      });  
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
