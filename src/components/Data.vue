<template>
    <h1>Scores</h1>
    <div v-for="score in scores" :key="score.Name">
        <h2>{{score.Name}}</h2>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                scores: []
            }
        },
        mounted() {
            fetch("https://localhost:44376/api/scores")
                .then(res => res.json())
                .then(data => this.scores = data)
                .catch(err => console.log(err.message))
        }
    }
</script>