<template>
    <v-app id="inspire" dark>
        <v-content>
            <v-container fluid fill-height>
                <v-layout align-bottom justify-center>
                    <v-snackbar v-model="snackbar_created" :timeout="1200" top>Delivery Note is Created</v-snackbar>  <!-- Enimerwsi oti egine created-->
                    <v-flex xs10 sm10 md10 lg10 xl10>
                        <v-card class="elevation-24">
                            <v-toolbar dark color="success">
                                <v-toolbar-title>ΔΕΛΤΙΟ ΑΠΟΣΤΟΛΗΣ</v-toolbar-title>
                            </v-toolbar>
                            <v-card-text>
                                <v-form>
                                    <v-text-field prepend-icon="person" type="text" name="company_name" v-model="company_name" placeholder="ΕΠΩΝΥΜΙΑ" />
                                    <v-layout row wrap>
                                        <v-flex xs6 sm6 md6 lg6 xl6>
                                            <v-text-field prepend-icon="work" type="text" name="job" v-model="job" placeholder="ΕΠΑΓΓΕΛΜΑ" />
                                            <v-text-field prepend-icon="home" type="text" name="address" v-model="address" placeholder="ΔΙΕΥΘΥΝΣΗ" />
                                            <v-text-field prepend-icon="open_in_browser" type="text" name="place_of_loading" v-model="place_of_loading" placeholder="ΤΟΠΟΣ ΦΟΡΤΩΣΗΣ" />
                                            <v-text-field prepend-icon="room" type="text" name="destination" v-model="destination" placeholder="ΠΡΟΟΡΙΣΜΟΣ" />
                                        </v-flex>
                                        <v-flex xs6 sm6 md6 lg6 xl6>
                                            <v-text-field prepend-icon="description" type="text" name="afm" v-model="afm" placeholder="ΑΦΜ" />
                                            <v-select dense prepend-icon="store" autocomplete :items="city" placeholder="City" editable v-model="city1"/>
                                            <v-text-field prepend-icon="assignment" type="text" name="doy" v-model="doy" placeholder="ΔΟΥ" />
                                            <div class="large-12 medium-12 small-12 cell">
                                                <label>ΑΡΧΕΙΟ ΠΑΡΑΓΓΕΛΙΑΣ
                                                    <input type="file" id="file" ref="file"/>
                                                </label>
                                            </div>
                                        </v-flex>
                                        <v-flex xs6 sm6 md6 lg12 xl6>
                                            <v-data-table hide-actions flat :headers="headers" :items="details" height="3">
                                                <template flat slot="headerCell" slot-scope="props">
                                                    <span>{{ props.header.text }}</span>
                                                </template>
                                                <template slot="items" slot-scope="props">
                                                    <td><v-text-field type="text" placholder="1" hide-details v-model="props.item[0]"></v-text-field></td>
                                                    <td><v-text-field type="text" placholder="2" hide-details v-model="props.item[1]"></v-text-field></td>
                                                    <td><v-text-field type="text" placholder="3" hide-details v-model="props.item[2]"></v-text-field></td>
                                                    <td><v-text-field type="text" placholder="4" hide-details v-model="props.item[3]"></v-text-field></td>
                                                    <td><v-text-field type="text" placholder="5" hide-details v-model="props.item[4]"></v-text-field></td>
                                                </template>
                                            </v-data-table>
                                        </v-flex>
                                    </v-layout>
                                </v-form>
                            </v-card-text>
                            <v-card-actions>
                                <v-btn color="success" @click="submit()">SUBMIT</v-btn>
                                <v-spacer></v-spacer>
                                <v-btn color="primary" @click="add_row()">ADD NEW ROW</v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-content>
    </v-app>
</template>

<script>
import Autocomplete from 'v-autocomplete'
import BackEndApi from '../services/api/backEnd';
import axios from 'axios';

export default {
    name: 'Homepage',
    data() {
        return {
            snackbar_created: false,
            company_name: "awe",
            job: "bwe",
            address: "cwe",
            place_of_loading: "dwe",
            destination: "ewe",
            afm: "12345678901",
            city1: "Larissa",
            city: ['Athens',
                'Thessaloniki',
                'Patras',
                'Piraeus',
                'Larissa',
                'Heraklion',
                'Peristeri',
                'Kallithea',
                'Acharnes',
                'Kalamaria',
                'Nikaia',
                'Glyfada',
                'Volos',
                'Ilio',
                'Ilioupoli',
                'Keratsini',
                'Evosmos',
                'Chalandri',
                'Nea Smyrni',
                'Marousi',
                'Agios Dimitrios',
                'Zografou',
                'Egaleo',
                'Nea Ionia',
                'Ioannina',
                'Palaio Faliro',
                'Korydallos',
                'Trikala',
                'Vyronas',
                'Agia Paraskevi',
                'Galatsi',
                'Agrinio',
                'Chalcis',
                'Petroupoli',
                'Serres',
                'Alexandroupoli',
                'Xanthi',
                'Katerini',
                'Kalamata',
                'Kavala',
                'Chania',
                'Lamia',
                'Komotini',
                'Irakleio',
                'Rhodes',
                'Kifissia',
                'Stavroupoli',
                'Chaidari',
                'Drama',
                'Veria',
                'Alimos',
                'Kozani',
                'Polichni',
                'Karditsa',
                'Sykies',
                'Ampelokipoi',
                'Pylaia',
                'Agioi Anargyroi',
                'Argyroupoli',
                'Ano Liosia',
                'Nea Ionia',
                'Rethymno',
                'Ptolemaida',
                'Tripoli',
                'Cholargos',
                'Vrilissia',
                'Aspropyrgos',
                'Corinth',
                'Gerakas',
                'Metamorfosi',
                'Giannitsa',
                'Voula',
                'Kamatero',
                'Mytilene',
                'Neapoli',
                'Eleftherio-Kordelio',
                'Chios',
                'Agia Varvara',
                'Kaisariani',
                'Nea Filadelfeia',
                'Moschato',
                'Perama',
                'Salamina',
                'Eleusis',
                'Corfu',
                'Pyrgos',
                'Megara',
                'Kilkis',
                'Dafni',
                'Thebes',
                'Melissia',
                'Argos',
                'Arta',
                'Artemida',
                'Livadeia',
                'Pefki',
                'Oraiokastro',
                'Aigio',
                'Kos',
                'Koropi',
                'Preveza',
                'Naousa',
                'Orestiada',
                'Peraia',
                'Edessa',
                'Florina',
                'Panorama',
                'Nea Erythraia',
                'Elliniko',
                'Amaliada',
                'Pallini',
                'Sparta',
                'Agios Ioannis Rentis',
                'Thermi',
                'Vari',
                'Nea Makri',
                'Tavros',
                'Alexandreia',
                'Menemeni',
                'Paiania',
                'Kalyvia Thorikou',
                'Nafplio',
                'Drapetsona',
                'Efkarpia',
                'Papagou',
                'Nafpaktos',
                'Kastoria',
                'Grevena',
                'Pefka',
                'Nea Alikarnassos',
                'Missolonghi',
                'Gazi',
                'Ierapetra',
                'Kalymnos',
                'Rafina',
                'Loutraki',
                'Agios Nikolaos',
                'Ermoupoli',
                'Ialysos',
                'Mandra',
                'Tyrnavos',
                'Glyka Nera',
                'Ymittos',
                'Neo Psychiko'],
            doy: "hwe",
            headers: [
                {
                    text: "ΠΕΡΙΓΡΑΦΗ ΑΓΑΘΩΝ",
                    align: "center",
                    sortable: true,
                    value: "name",
                    width: "600px"
                },
                {
                    text: "Μ.Μ",
                    value: "min",
                    sortable: true,
                    align: "center"
                },
                {
                    text: "ΠΟΣΟΤΗΣ",
                    value: "mean",
                    sortable: true,
                    align: "center"
                },
                {
                    text: "ΤΙΜΗ ΜΟΝΑΔΑΣ",
                    value: "max",
                    sortable: true,
                    align: "center"
                },
                {
                    text: "ΦΠΑ",
                    value: "max",
                    sortable: true,
                    align: "center"
                }
            ],
            details: [],
            file: ''
        };
    },
    created () {
        const token = localStorage.getItem('access_token')
        axios.defaults.headers.common['Authorization'] = token
        console.log(token)
        this.init_details()
    },
    methods: {
        submit() {
            const token = localStorage.getItem('access_token')
            axios.defaults.headers.common['Authorization'] = token
            this.file = this.$refs.file.files[0];
            // console.log(this.details)
            let formData = new FormData();
            formData.append('file', this.file);
            formData.set('name',this.company_name);
            formData.set('job',this.job);
            formData.set('VatRegistrationNum',this.afm);
            formData.set('address',this.address);
            formData.set('city',this.city1);
            formData.set('loadingPlace',this.place_of_loading);
            formData.set('taxOffice',this.doy);
            formData.set('destination',this.destination);
            // formData.set('details',this.details);
            axios.post('http://localhost:5000/deliveryNotes/createDeliveryNote/', formData,
                { headers: {'Content-Type': 'multipart/form-data'}}
            )
            .then(response => {
                console.log(response)
                console.log('Delivery Note created!');
                this.snackbar_created = true;
            })
            .catch(function(error) {
                console.log(error);
            });
        },
        init_details() {
            this.details = [{},{},{},{},{}];
        },
        add_row() {
            this.details.push({});
        }
    }
}
</script>

<style scoped>
    #secure {
        background-color: #FFFFFF;
        border: 1px solid #CCCCCC;
        padding: 20px;
        margin-top: 10px;
    }
</style>
