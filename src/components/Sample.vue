<template>
 <div class="sample">
  <h1>{{title}}</h1>
  <svg></svg>
 </div>
</template>

<script>
import * as d3 from 'd3';
import { datamuc } from './datamuc.js';

export default {
    name: 'Sample',
    props: {
        title: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            _list: [1.1, 2.2, 3.4, 4.1, 8.5, 9.9, 7.1, 8.8, 9.4],
            list: datamuc
        };
    },

    mounted() {
        const height = 3000;
        const width = 2000;

        const max = d3.max(datamuc, d => d['hauptwohnsitzbevölkerung']);
        const svg = d3
            .select('svg')
            .attr('height', height)
            .attr('width', width);

        const scaleFactor = 1300 / max;

        svg
            .selectAll(null)
            .data(datamuc)
            .enter()
            .append('g');

        svg
            .selectAll('g')
            .append('rect')
            .attr('x', -20)
            .attr('y', function(d, i) {
                return i * 25;
            })
            .attr('rx', 10)
            .attr('ry', 10)
            .attr('width', 0)
            .attr('height', 20)
            .style('opacity', 0.6)
            .style('fill', function(d, i) {
                return d3.rgb(i * 10, 90 + i * 2, 150);
            })
            .on('mouseover', function(d, i) {
                d3
                    .selectAll('rect')
                    .transition()
                    .duration(300)
                    .style('opacity', 0.6);

                d3
                    .select(this)
                    .transition()
                    .duration(300)
                    .style('opacity', 1);

                const posx = +d3.select(this).attr('width') + 10;

                d3
                    .selectAll('text')
                    .filter(function(k, j) {
                        return j === i;
                    })
                    .transition()
                    .duration(500)
                    .delay(200)
                    .attr('x', posx)
                    .text(function(d, i) {
                        return `${d.bezirksteil_bezeichnung.substr(
                            5
                        )} (${d.hauptwohnsitzbevölkerung} Hauptwohnsitze)`;
                    })
                    .style('opacity', 1);
            })

            .on('mouseout', function(d, i) {
                let posx = +d3.select(this).attr('width');

                d3
                    .selectAll('text')
                    .filter(function(k, j) {
                        return j === i;
                    })
                    .transition()
                    .duration(500)
                    .attr('x', posx)
                    .text(function(d, i) {
                        return `${d.bezirksteil_bezeichnung.substr(5)}`;
                    })
                    .style('opacity', 0.2);
            })

            .transition()
            .duration(1000)
            .attr('width', function(d) {
                return 100 + scaleFactor * d['hauptwohnsitzbevölkerung'];
            });

        svg
            .selectAll('g')
            .append('text')
            .attr('y', function(d, i) {
                return 15 + i * 25;
            })
            .style('opacity', 0)
            .attr('x', function(d) {
                return 125 + scaleFactor * d['hauptwohnsitzbevölkerung'];
            })
            .transition()
            .duration(300)
            .delay(1000)
            .attr('x', function(d) {
                return 100 + scaleFactor * d['hauptwohnsitzbevölkerung'];
            })
            .style('opacity', 0.2)
            .style('fill', 'white')
            .text(function(d, i) {
                return `${d.bezirksteil_bezeichnung.substr(5)}`;
            });
    }
};
</script>

<style lang="scss">
.sample {
    // background: linear-gradient(to bottom, rgba(233, 180, 0, 0.3), rgba(233, 180, 255, 0.4));
    background-color: rgb(31, 31, 31);
    padding-top: 100px;
    
    h1{
        margin-bottom:100px;
        opacity: .8;
        color: white;
    }
}

</style>