<template>
 <div>
  <h1>{{title}}</h1>
  <svg height="500" width="800"></svg>
 </div>
</template>

<script>
import * as d3 from 'd3';
const data = [4, 8, 15, 16, 23, 42];
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
           list: [1, 2, 3, 4, 8.5, 11, 7, 8, 9],
        };
    },

    mounted() {
        const max = Math.max(...this.list) + 2;
        this.list.forEach((number, i) =>  {
            const group = d3.select('svg').append('g').attr('id', 'group_' + number);
            group.append('rect')
            .attr('x', 75)
            .attr('y', i * 25)
            .attr('rx', 10)
            .attr('ry', 10)
            .attr('width', 50 * number)
            .attr('height', 20)
            .style('fill', d3.rgb(233, 180, i * 30))

            group.append('rect')
            .attr('x', 75)
            .attr('y', i * 25)
            .attr('rx', 10)
            .attr('ry', 10)
            .attr('width', 50 * max)
            .attr('height', 20)
            .style('opacity', .2)
            .style('fill', d3.rgb(233, 180, i * 30))

            group.append('text')
            .attr('x', 0)
            .attr('y', 15 + i * 25)
            .text(`value ${number}`)
        });
        
    },
};
</script>

<style lang="sass">
svg
    margin: 25px


</style>