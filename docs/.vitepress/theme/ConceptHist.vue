<script>
import { withBase } from 'vitepress'
import * as Plot from "@observablehq/plot";

export default {
    props: {
        curConcepts: Object,
        key: Number,
    },
    mounted() {
        const data = this.curConcepts.data;
        const plot = Plot.plot({
            marks: [
                Plot.gridY(),
                Plot.barY(data, {
                    x: 'name', 
                    y: 'n', 
                    fill: 'fill', 
                    tip: { format: { fill: null }}, 
                    sort: { x: "y", reverse: true, limit: 20 }
                }),
                Plot.axisX({
                    label: "",
                    lineWidth: 5,
                }),
                Plot.axisY({
                    label: "Number of documents",
                    // percent: true,
                })
            ],
            marginBottom: 50,
            width: 400,
            height: 135,
            style: { fontSize: 11}
        });
        this.$refs.view.replaceChildren(plot);
    }
}
</script>

<template>
    <div class="plot" ref="view">
        <em>Loading Example...</em>
    </div>
</template>

<style>
.plot {
    margin-top: 5px;
    margin-bottom: 5px;
}
</style>
