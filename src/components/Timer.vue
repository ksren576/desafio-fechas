<template>
    <div>
        <h1>Cuenta regresiva</h1>
        <h2>{{ mostrarTemporizador }}</h2>
        <div class="botonera">
            <button @click="setearTemporizador(0)">3 s</button>
            <button @click="setearTemporizador(1)">1 m</button>
            <button @click="setearTemporizador(2)">5 m</button>
            <button @click="setearTemporizador(3)">10 m</button>
            <button @click="setearTemporizador(4)">30 m</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Timer',
        data() {
            return {
                valorBotones: [3, 60, 300, 600, 1800],
                temporizador: new Date('2021-01-01 00:00:00'),
                intervalo: null,
            }
        },
        methods: {
            setearTemporizador(indice) {
                const objetoFecha = new Date('2021-01-01 00:00:00');
                const segundosParaAgregar = this.valorBotones[indice];
                objetoFecha.setSeconds(segundosParaAgregar);
                this.temporizador = new Date(objetoFecha);
                if (this.intervalo) clearInterval(this.intervalo);
                this.intervalo = setInterval(() => {
                    const segundosActuales = this.temporizador.getSeconds();
                    const minutosActuales = this.temporizador.getMinutes();
                    if (segundosActuales !== 0 || minutosActuales !== 0) {
                        this.temporizador.setSeconds(segundosActuales - 1);
                        this.temporizador = new Date(this.temporizador);
                    }
                }, 1000)
            }
        },
        computed: {
            mostrarTemporizador() {
                return `${this.temporizador.getMinutes()}:${this.temporizador.getSeconds()} min/seg`;
            }
        },
    }
</script>

<style scoped>
    button {
        margin: 0 10px;
    }
</style>