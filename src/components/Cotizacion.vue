<script setup>
defineProps({
	cotizacion: {
		type: Object,
		required: true,
	},
})
</script>
import useCripto from '../composables/useCripto';

<template>
	<div class="contenedor-resultado">
		<h2>Cotizacion</h2>
		<div class="resultado">
			<img
				:src="'https://cryptocompare.com/' + cotizacion.IMAGEURL"
				alt="imagen cripto"
			/>
			<div>
				<p>
					El precio es de: <span>{{ cotizacion.PRICE }}</span>
				</p>
				<p>
					Precio mas alto del dia: <span>{{ cotizacion.HIGHDAY }}</span>
				</p>
				<p>
					Precio mas bajo del dia: <span>{{ cotizacion.LOWDAY }}</span>
				</p>
				<p>
					Variacion ultimas 24 horas:
					<span>{{ cotizacion.CHANGEPCT24HOUR }}%</span>
				</p>
				<p>
					Ultima actualizacion: <span>{{ cotizacion.LASTUPDATE }}</span>
				</p>
			</div>
		</div>
	</div>
</template>

<style lang="scss" scoped></style>
