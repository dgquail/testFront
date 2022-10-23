<template>
    <div class="card">
        <div class="card-header">
            Agregar / Editar Noticia
        </div>
        <div class="card-body">
            <form v-on:submit.prevent="guardarNoticia">
                <div class="mb-3">
                    <label for="" class="form-label">Contenido</label>
                    <input type="text" class="form-control" name="" id="contenido" aria-describedby="helpId"
                        placeholder="Escriba el contenido de la noticia" required v-model="noticia.contenido">
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">Categoria</label>
                    <select class="form-select" name="" id="categoria" v-model="noticia.categoria" required>
                        <option v-for="categoria in categorias" :key="categoria.id" :value="categoria.id">
                            {{categoria.nombre}}</option>
                    </select>
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">Region</label>
                    <select class="form-select" name="" id="region" v-model="noticia.region">
                        <option v-for="region in regiones" :key="region.id" :value="region.id">{{region.nombre}}
                        </option>
                    </select>
                </div>
                <button type="submit" class="btn btn-primary">Guardar</button>
                <button class="btn">Cancelar</button>
            </form>
        </div>

    </div>
</template>
<script>
export default {
    data() {
        return {
            noticia: {},
            categorias: [],
            regiones: [],
        }
    },
    created: function () {
        this.getCategorias();
        this.getRegiones();
    },
    methods: {
        getCategorias() {
            const options = { method: 'GET', headers: { Accept: 'application/json' } };
            fetch('http://127.0.0.1:8000/api/categorias', options)
                .then(response => response.json())
                .then(response => {
                    this.categorias = response;
                })
                .catch(err => console.error(err));
        },
        getRegiones() {
            const options = { method: 'GET', headers: { Accept: 'application/json' } };
            fetch('http://127.0.0.1:8000/api/regions', options)
                .then(response => response.json())
                .then(response => {
                    this.regiones = response;
                })
                .catch(err => console.error(err));
        },
        guardarNoticia() {
            console.log(this.noticia);
        }
    }
}
</script>
