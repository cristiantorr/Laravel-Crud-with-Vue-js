<template>
    <div class="card">
        <div class="card-header">¿En que estás pensando ahora?</div>
        <div class="card-body">
            <form action="" v-on:submit.prevent="newThought()">
                <div class="form-group">
                    <label for="">Ahora estoy pensando en:</label>
                    <input type="text" class="form-control" id="thought" name="thought" placeholder="En una vaca" v-model="description">
                    <small id="" class="form-text text-muted">Que sean pensamientos algo locos por favor...!.</small><br />
                    <button type="submit" class="btn btn-primary">
                        Enviar pensamiento
                    </button>
                </div>
            </form>    
        </div>
    </div>
</template>

<script>
    export default {

        data() {
            return {
                description: ''
            }
        },

        mounted() {
            console.log('Component mounted.')
        },
        methods: {
            newThought() {
                const params = {
                    description: this.description
                };

               axios.post('/thoughts', params)
                .then((response) => {
                    const thought = response.data;
                    this.$emit('new', thought);
                });
            }
        }
    }
</script>
