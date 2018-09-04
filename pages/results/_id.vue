<template>
    <div>
    <h1>Resultados para {{$route.params.id}}</h1>

    <div v-if="albumExists">
    <div v-for="(album, index) in albumData">
        <Card
        :title="album.collectionCensoredName"
        :image="album.artworkUrl100"
        :artistName="album.artistName"
        :url="album.artistViewUrl"
        :color="picker(index)"
        />
    </div>
  
    {{albumData}}
        </div>
        <div v-else>

        <h1>No se puede Cargar</h1>
        </div>
    </div>
</template>
<script>
import axios from 'axios';
import Card from '~/components/Card.vue';
export default {
    asyncData({params}){
    return axios.get(`https://itunes.apple.com/search?term=${params.id}&entity=album`)
    .then((response) => {
      return {albumData: response.data.results}
    });
    },
    components: { 
        Card
    },
        middleware: 'search',
        methods: {
            picker(index){
                return index % 2 == 0 ? 'red' : 'blue';
            }
        },
        computed: {
            albumExists(){
                return this.albumData.length  >0;
            }
        }
}
</script>