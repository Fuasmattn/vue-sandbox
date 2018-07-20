<template>
 <div>
  <h1>{{title}}</h1>
  <svg height="5000" width="1200"></svg>
 </div>
</template>

<script>
import * as d3 from 'd3';
import {datamuc} from './datamuc.js';

export default {
    name: 'Sample',
    props: {
        title: {
            type: String,
            required: true,
        },
    },
    data() {
        return {
           _list: [1.1, 2.2, 3.4, 4.1, 8.5, 9.9, 7.1, 8.8, 9.4],
            list: datamuc
        };
    },

    mounted() {
        const max = Math.max(...this.list.map(it => it.hauptwohnsitzbevölkerung)) + 2;
        const factor = 1100 / max;
        this.list.forEach((item, i) =>  {
            console.log(factor * item.hauptwohnsitzbevölkerung);
            const group = d3.select('svg')
            .append('g').attr('id', 'group_' + item.bezirksteil);

            group.append('rect')
            .attr('x', 75)
            .attr('y', i * 25)
            .attr('rx', 10)
            .attr('ry', 10)
            .attr('width', 0)
            .attr('height', 20)
            .style('fill', d3.rgb(233, 180, i * 3))
            .transition()
            //.delay((max - item.bezirksteil) * 50)
            .duration(1000)
            .attr("width", factor * item.hauptwohnsitzbevölkerung)

            group.append('rect')
            .attr('x', 75)
            .attr('y', i * 25)
            .attr('rx', 10)
            .attr('ry', 10)
            .attr('width', factor * max)
            .attr('height', 20)
            .style('opacity', .2)
            .style('fill', d3.rgb(233, 180, i * 30))

            group.append('text')
            .attr('x', 90)
            .attr('y', 15 + i * 25)
            .text(`${item.bezirksteil_bezeichnung.substr(5)}: ${item.hauptwohnsitzbevölkerung}`)
            .style('opacity', 0)
            .transition()
            .duration(1000)
            .style('opacity', 0.5)
        });
        
    },
};
</script>

<style lang="sass">
svg
    margin: 25px


</style>