<template>
    <div class="container">
        <div class="card">
            <div class="card-header">
            Editar Empleado

            </div>
            <div class="card-body">

                <form v-on:submit.prevent="actualizarRegistro">
                        <div class="mb-3">
                          <label for="nombre" class="form-label">Nombre</label>
                          <input type="text"
                            class="form-control" name="nombre" id="nombre" v-model="empleado.nombre" aria-describedby="helpId" placeholder="Escribe tu nombre" required >
                          <small id="helpId" class="form-text text-muted">Este campo es obligatorio</small>
                        </div>
                        <div class="mb-3">
                          <label for="correo" class="form-label">Correo electrónico</label>
                          <input type="email"
                            class="form-control" name="correo" v-model="empleado.correo" id="correo" aria-describedby="helpId" placeholder="Escribe tu correo" required >
                          <small id="helpId" class="form-text text-muted">Este campo es requerido </small>
                        </div>

                        <div class="btn-group" role="group" aria-label="">
                            <button type="submit" class="btn btn-success">Modificar</button>
                            <!-- <button type="button" class="btn btn-danger">Cancelar</button> -->
                            <router-link :to="{name:'Listar'}" class="btn btn-warning">Cancelar</router-link>
                        </div>
                </form>
            </div>
           
        </div>
    </div>
</template>

<script>
export default {
    data(){
     return{
         empleado:{}
     }
    },

    created:function(){
        this.obtenerInformacionID();
    },
    methods:{
      obtenerInformacionID(){
            fetch('http://localhost/empleados/?consultar='+this.$route.params.id)
                .then(respuesta => respuesta.json())
                .then((datosRespuesta)=>{
                       console.log(datosRespuesta)
                         this.empleado=datosRespuesta[0];
                })
                .catch(console.log)
      },
       actualizarRegistro(){

            var datosEnviar={id:this.$route.params.id,nombre:this.empleado.nombre,correo:this.empleado.correo}

            fetch('http://localhost/empleados/?actualizar='+this.$route.params.id,{
                method:'POST',
                body:JSON.stringify(datosEnviar)

            })
        .then(respuesta=>respuesta.json())
        .then((datosRespuesta=>{
            console.log(datosRespuesta);
            window.location.href='../listar'
        }))
      }
    }
//reutilizamos el codigo de la funcion agregarRegistro de crear
   
}
</script>