<template lang="pug">

    .card.artist
        .card-image
            figure(class="image is-4by3")
                img(:src="artist.image[3]['#text']" :alt="artist.name")
        .card-content
            .media
                .media-left
                    figure(class="image is-48x48")
                        img(:src="artist.image[1]['#text']" :alt="artist.name")
                .media-content
                    p(class="title is-4") {{ artist.name }}
                    p(class="subtitle is-7") @{{ artist.name }}
        footer(class="card-footer")
            a(:href="artist.url" class="card-footer-item" target="_blank") Ver Artista en Last.fm

</template>

<script>
export default {
    name: "artist",
    props: ["artist"]
};
</script>

<style lang="stylus" scoped>
.artist {
    display: inline-block;
    margin: 10px 5px;
    width: 300px;
}
</style>
