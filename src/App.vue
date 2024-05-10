<script setup>
import { ref, reactive, computed } from 'vue'
import useCripto from './composables/useCripto'
import Alerta from './components/Alerta.vue'
import Spinner from './components/Spinner.vue'
import Cotizacion from './components/Cotizacion.vue'

const {
	monedas,
	criptomonedas,
	cargando,
	cotizacion,
	obtenerCotizacion,
	mostrarResultado,
} = useCripto()

const cotizar = reactive({
	moneda: '',
	criptomoneda: '',
})
const error = ref('')

const cotizarCripto = () => {
	if (Object.values(cotizar).includes('')) {
		error.value = 'Todos los campos son obligatorios'
		return
	}

	error.value = ''
	obtenerCotizacion(cotizar)
}
</script>

<template>
	<div class="contenedor">
		<h1 class="titulo">Cotizador de <span>criptomonedas</span></h1>
		<div class="contenido">
			<Alerta v-if="error">{{ error }}</Alerta>
			<form @submit.prevent="cotizarCripto" class="formulario">
				<div class="campo">
					<label for="moneda">Moneda:</label>
					<select v-model="cotizar.moneda" id="moneda">
						<option value="">-- Selecciona --</option>
						<option
							v-for="moneda in monedas"
							:key="moneda.codigo"
							:value="moneda.codigo"
						>
							{{ moneda.texto }}
						</option>
					</select>
				</div>

				<div class="campo">
					<label for="criptomoneda">Criptomoneda:</label>
					<select v-model="cotizar.criptomoneda" id="criptomoneda">
						<option value="">-- Selecciona --</option>
						<option
							v-for="criptomoneda in criptomonedas"
							:key="criptomoneda.CoinInfo"
							:value="criptomoneda.CoinInfo.Name"
						>
							{{ criptomoneda.CoinInfo.FullName }}
						</option>
					</select>
				</div>

				<input type="submit" value="cotizar" />
			</form>

			<Spinner v-if="cargando" />
			<Cotizacion v-if="!mostrarResultado" :cotizacion="cotizacion" />
		</div>
	</div>
</template>
