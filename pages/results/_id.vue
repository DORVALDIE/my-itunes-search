<template>
    <div>
    <h1>Hola desde la ruta de resultados {{$route.params.id}}</h1>
    <h2>Datos del Album</h2>
    {{albumData}}
    </div>
</template>
<script>
import axios from 'axios';
export default {
    asyncData(params){
    return axios.get(`https://itunes.apple.com/search?term=${params.id}&entity=album`)
    .then((response) => {
      return {albumData: response.data.results}
    });
    },
        middleware: 'search'
}
</script>