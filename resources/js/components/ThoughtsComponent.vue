<template>
    <div class="card text-center">
        <div class="card-header">Nombre de quíen uso el pensamiento: {{ thought.name }}</div>
        <div class="card-body">
            <input v-if="editMode" type="text" class="form-control"  placeholder="Descripción" v-model="thought.description">
             <p class="card-text" v-else>{{ thought.description }}</p>
             <button v-if="editMode" type="submit" class="btn btn-primary" v-on:click="onclickUpdate()" >Guardar Cambios</button>
            <button type="submit" class="btn btn-primary" v-on:click="onclickEdit()" v-else>Editar</button>
            <button type="submit" class="btn btn-danger" v-on:click="onclickDelete()">Eliminar</button>
        </div>
        <div class="card-footer text-muted">
            {{ thought.created_at }} - Última actualización: {{ thought.updated_at }}
        </div>
    </div>
</template>

<script>
    export default {
        props: ['thought'],
        data () {
            return {
                editMode: false
            };
        },

        mounted() {
            console.log('Component mounted.')
        },
        
        methods: {
            onclickDelete() {
               
                axios.delete(`/thoughts/${this.thought.id}`).then(() => { 
                    this.$emit('delete');
                });
            },

            onclickEdit() {
                this.editMode = true;
                // console.log('edit');
            },
            
            onclickUpdate() {
                const params = {
                    description: this.thought.description
                };

                axios.put(`/thoughts/${this.thought.id}`, params).then((response) => {
                    this.editMode = false;
                    const thought =  response.data;
                    this.$emit('update', thought);
                });
            }
        }
        
    }
</script>
