<template>
	<v-container>
		<v-row
		justify="space-around"
		align="center"
		>
		<v-time-picker
		v-model="wib"
		format="24hr"
		color="deep-purple"
		readonly
		></v-time-picker>
		<v-time-picker
		v-model="wita"
		format="24hr"
		color="deep-purple"
		readonly
		placeholder="WITA"
		></v-time-picker>
		<v-time-picker
		v-model="wit"
		format="24hr"
		color="deep-purple"
		readonly
		></v-time-picker>
	</v-row>
	<v-row class="text-center">
		<v-col cols="12">
			<v-card color="basil">
				<v-card-title class="text-center justify-center py-6">
					<h1 class="font-weight-bold display-3 basil--text">
						Data Gempa
					</h1>
				</v-card-title>

				<v-tabs
				v-model="tab"
				background-color="transparent"
				color="basil"
				grow
				>
				<v-tab
				v-for="item in items"
				:key="item"
				>
				{{ item }}
			</v-tab>
		</v-tabs>

		<v-tabs-items v-model="tab">
			<v-tab-item
			v-for="item in items"
			:key="item"
			>
			<v-card
			color="basil"
			flat
			>
			<v-simple-table light v-if="item==='Gempa Terbaru'">
				<template v-slot:default>
					<thead>
						<tr>
							<th>Tanggal</th>
							<th>Jam</th>
							<th>Datetime</th>
							<th>Magnitude</th>
							<th>Kedalaman</th>
							<th>Koordinat</th>
							<th>Lintang</th>
							<th>Bujur</th>
							<th>Wilayah</th>
							<th>Potensi</th>
							<th>Dirasakan</th>
							<th>Shakemap</th>
						</tr>
					</thead>
					<tbody>
						<tr v-for="n in gempan" :key="n.id">
							<td>{{n.Tanggal}}</td>
							<td>{{n.Jam}}</td>
							<td>{{n.DateTime}}</td>
							<td>{{n.Magnitude}}</td>
							<td>{{n.Kedalaman}}</td>
							<td>{{n.point.coordinates}}</td>
							<td>{{n.Lintang}}</td>
							<td>{{n.Bujur}}</td>
							<td>{{n.Wilayah}}</td>
							<td>{{n.Potensi}}</td>
							<td>{{n.Dirasakan}}</td>
						<td>
							<div class="text-center">
								<v-dialog
								v-model="dialog"
								width="500"
								>
								<template v-slot:activator="{ on, attrs }">
									<v-btn
									color="red lighten-2"
									dark
									v-bind="attrs"
									v-on="on"
									>
									Lihat map
								</v-btn>
							</template>

							<v-card dark>
								<v-img dark :src="`https://data.bmkg.go.id/DataMKG/TEWS/${n.Shakemap}`" width="100%" height="auto" alt="Gempa Bumi"></v-img>
								<v-card-actions>
									<v-spacer></v-spacer>
									<v-btn
									color="primary"
									text
									@click="dialog = false"
									>
									Close
								</v-btn>
							</v-card-actions>
						</v-card>
					</v-dialog>
				</div>
			</td>
		</tr>
	</tbody>
</template>
</v-simple-table>
<v-simple-table light v-if="item==='Gempa Terkini'">
	<template v-slot:default>
		<thead>
			<tr>
				<th>Tanggal</th>
				<th>Jam</th>
				<th>Datetime</th>
				<th>Magnitude</th>
				<th>Kedalaman</th>
				<th>Koordinat</th>
				<th>Lintang</th>
				<th>Bujur</th>
				<th>Wilayah</th>
				<th>Potensi</th>
			</tr>
		</thead>
		<tbody>
			<tr v-for="t in gempat" :key="t.id">
				<td>{{t.Tanggal}}</td>
				<td>{{t.Jam}}</td>
				<td>{{t.DateTime}}</td>
				<td>{{t.Magnitude}}</td>
				<td>{{t.Kedalaman}}</td>
				<td>{{t.point.coordinates}}</td>
				<td>{{t.Lintang}}</td>
				<td>{{t.Bujur}}</td>
				<td>{{t.Wilayah}}</td>
				<td>{{t.Potensi}}</td>
			</tr>
		</tbody>
	</template>
</v-simple-table>
<v-simple-table light v-if="item==='Gempa Dirasakan'">
	<template v-slot:default>
		<thead>
			<tr>
				<th>Tanggal</th>
				<th>Jam</th>
				<th>Datetime</th>
				<th>Magnitude</th>
				<th>Kedalaman</th>
				<th>Koordinat</th>
				<th>Lintang</th>
				<th>Bujur</th>
				<th>Wilayah</th>
				<th>Dirasakan</th>
			</tr>
		</thead>
		<tbody>
			<tr v-for="dr in gempadr" :key="dr.id">
				<td>{{dr.Tanggal}}</td>
				<td>{{dr.Jam}}</td>
				<td>{{dr.DateTime}}</td>
				<td>{{dr.Magnitude}}</td>
				<td>{{dr.Kedalaman}}</td>
				<td>{{dr.point.coordinates}}</td>
				<td>{{dr.Lintang}}</td>
				<td>{{dr.Bujur}}</td>
				<td>{{dr.Wilayah}}</td>
				<td>{{dr.Dirasakan}}</td>
			</tr>
		</tbody>
	</template>
</v-simple-table>
</v-card>
</v-tab-item>
</v-tabs-items>
</v-card>
</v-col>
</v-row>
</v-container>
</template>
<script>

import axios from 'axios'

export default {
	name: 'Gempa',
	data: function(){
		return {
			gempan : this.gempan,
			gempat : this.gempat,
			gempadr : this.gampadr,
			tab: null,
			items: [
			'Gempa Terbaru', 'Gempa Terkini', 'Gempa Dirasakan',
			],
			dialog: false,
			wib: this.wib,
			wita: this.wita,
			wit: this.wit,
			titleZone:''
		}
	},
	mounted(){
		this.gmp()
		this.zonewktid()		
	},
	destroyed(){
		clearInterval(this.interval)
	},
	methods: {
		async gmp(){
			var parseString = require('xml2js').parseString
			var urlgmpn = `https://data.bmkg.go.id/DataMKG/TEWS/autogempa.xml`
			var urlgmpt = `https://data.bmkg.go.id/DataMKG/TEWS/gempaterkini.xml`
			var urlgmpdr = `https://data.bmkg.go.id/DataMKG/TEWS/gempadirasakan.xml`
			const requestn = await axios.get(urlgmpn)
			const requestt = await axios.get(urlgmpt)
			const requestdr = await axios.get(urlgmpdr)
			var self = this;
			this.interval=setInterval(() => {
				parseString(requestn.data, {explicitArray : false}, function(err, result){
					self.gempan=JSON.parse(JSON.stringify(result["Infogempa"]))
				})
				parseString(requestt.data, {explicitArray : false}, function(err, result){
					self.gempat=JSON.parse(JSON.stringify(result["Infogempa"]["gempa"]))
				})
				parseString(requestdr.data, {explicitArray : false}, function(err, result){
					self.gempadr=JSON.parse(JSON.stringify(result["Infogempa"]["gempa"]))
				})
			}, 1000)
		}, 

		async zonewktid(){
			const moment = require('moment-timezone');
			var titleWib = document.getElementsByClassName('v-time-picker-title__time')[0]
			var textWib =  document.createTextNode('WIB')
			titleWib.appendChild(textWib)
			var titleWita = document.getElementsByClassName('v-time-picker-title__time')[1]
			var textWita =  document.createTextNode('WITA')
			titleWita.appendChild(textWita)
			var titleWit = document.getElementsByClassName('v-time-picker-title__time')[2]
			var textWit =  document.createTextNode('WIT')
			titleWit.appendChild(textWit)
			this.interval=setInterval(() => {
				this.wib = new Date(moment.tz('Asia/Jakarta').format('YYYY/MM/DD HH:mm:ss'))
				this.wita = new Date(moment.tz('Asia/Makassar').format('YYYY/MM/DD HH:mm:ss')) 
				this.wit = new Date(moment.tz('Asia/Jayapura').format('YYYY/MM/DD HH:mm:ss'))
			}, 1000)
		}
	}
};
</script>
<style scope>
/* Helper classes */
.basil {
	background-color: #FFFBE6 !important;
}
.basil--text {
	color: #356859 !important;
}
.v-data-table__wrapper {
	overflow-x: hidden !important;
}
</style>