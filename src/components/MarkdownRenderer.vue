<template>
    <div v-html="htmlContent"></div>
</template>

<script>
import { marked } from "marked";

export default {
    props: {
        markdownFile: {
            type: String,
            required: true,
        }
    },
    data() {
        return {
            htmlContent: "",
        };
    },
    mounted() {
        this.loadMarkdown();
    },
    methods: {
        async loadMarkdown() {
            try {
                const response = await fetch(this.markdownFile);
                const markdownText = await response.text();
                this.htmlContent = marked(markdownText);
            } catch (error) {
                console.error("Error loading markdown file:", error);
            }
        }
    }
}
</script>