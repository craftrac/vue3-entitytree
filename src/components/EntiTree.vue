<template>
    <div id="layertree" class="ptree">
        <ul :id="config.key + '_tree_picklemain'"></ul>
    </div>
</template>

<style scoped>
@import '../../public/css/style.css';

#layertree {
    background-color: white;
}    
</style>

<script setup>
import PickleTree from '../ptree.js';
import { onMounted } from 'vue';

const props = defineProps({
    c_data: {
        type: Object,
        required: true
    },
    config: {
        type: Object,
        default: {
            key: new Date().getTime(),
            //logs are open or close
            logMode: false,
            //switch mode
            switchMode: false,
            hasLink: false,
            //family mode
            //for child
            autoChild: true,
            //for parent
            autoParent: true,
            //fold icon
            foldedIcon: "fa fa-plus",
            //unfold icon
            unFoldedIcon: "fa fa-minus",
            //menu icon
            menuIcon: ["fa", "fa-list-ul"],
            //link icon
            linkIcon: "fa fa-list-ul",
            //start status is collapsed or not
            foldedStatus: false,
            //drag
            drag: false,
            //order
            order: false,
            // context menu position
            contextPos: 'after'
        }
    }
});

const myData = [{
      n_id: 1,
      n_title: 'MARINE AREAS',
      n_parentid: 0,
    },{
      n_id: 11,
      n_title: 'Assessment Areas',
      n_parentid: 1
    },{
      n_id: 111,
      n_title: 'Mediterranean Sea Region',
      code: "ms_el_mediterranean_assessment_area",
      n_parentid: 11
    },{
      n_id: 112,
      n_title: 'Adriatic Sea subregion',
      code: "mad_el_ms_ad_adriatic_assessment_area",
      n_parentid: 11
    },{
      n_id: 113,
      n_title: 'Ionian Sea and Central Mediterranean Sea subregion',
      code: "mic_el_ms_io_ionian_assessment_area",
      n_parentid: 11
    },{
      n_id: 114,
      n_title: 'Aegean-Levantine subregion',
      code: "mal_el_ms_al_aegean_levantine_assessment_area",
      n_parentid: 11
    },{
      n_id: 115,
      n_title: 'Aegean-Levantine subregion – Aegean Sea',
      code: "mal_el_aa_ae_aegean_assessment_area",
      n_parentid: 11
    },{
      n_id: 116,
      n_title: 'Aegean-Levantine subregion – North Aegean Sea',
      code: "mal_el_aa_na_north_aegean_assessment_area",
      n_parentid: 11
    },{
      n_id: 117,
      n_title: 'Aegean-Levantine subregion – Central and South Aegean Sea',
      code: "mal_el_aa_csa_central_south_aegean_assessment_area",
      n_parentid: 11
    },{
      n_id: 118,
      n_title: 'Aegean-Levantine subregion - Levantine Sea',
      code: "mal_el_aa_le_levantine_assessment_area",
      n_parentid: 11
    },{
      n_id: 12,
      n_title: 'Coastal Waters',
      code: "v_el_mrus_nov2021_epsg3035_coastal_waters",
      n_parentid: 1
    },{
      n_id: 16,
      n_title: 'Coastal Water Bodies (WFD)',
      code: "v_el_mrus_nov2021_epsg3035_coasts",
      n_parentid: 1
    },{
      n_id: 13,
      n_title: 'Territorial Waters',
      code: "v_el_mrus_nov2021_epsg3035_territorial",
      n_parentid: 1
    },{
      n_id: 14,
      n_title: 'Territorial Part beyond Coastal Waters',
      code: "v_el_mrus_nov2021_epsg3035_territorial_from_coastal",
      n_parentid: 1
    },{
      n_id: 15,
      n_title: 'Beyond Territorial Waters',
      code: "v_el_mrus_nov2021_epsg3035_beyond_territorial",
      n_parentid: 1
    },{
      n_id: 2,
      n_title: 'DATA SOURCES',
      n_parentid: 0,
    },{
      n_id: 21,
      n_title: 'MSFD MONITORING PROGRAMS',
      n_parentid: 2,
    },{
      n_id: 213,
      n_title: 'Beach Stations',
      code: "beach_stations",
      n_parentid: 21
    },{
      n_id: 211,
      n_title: 'MSFD Stations',
      code: "cruise_stations",
      n_parentid: 21
    },{
      n_id: 212,
      n_title: 'MSFD Cruises',
      n_parentid: 21
    },{
      n_id: 2121,
      n_title: 'Cruise 2018',
      code: "cruise_2018",
      n_parentid: 212
    },{
      n_id: 2122,
      n_title: 'Cruise 2019 A',
      code: "cruise_2019_a",
      n_parentid: 212
    },{
      n_id: 2123,
      n_title: 'Cruise 2019 B',
      code: "cruise_2019_b",
      n_parentid: 212
    },{
      n_id: 2124,
      n_title: 'Cruise 2020 A',
      code: "cruise_2020_a",
      n_parentid: 212
    },{
      n_id: 2125,
      n_title: 'Cruise 2020 B',
      code: "cruise_2020_b",
      n_parentid: 212
    },{
      n_id: 2126,
      n_title: 'Cruise 2021 A',
      code: "cruise_2021_a",
      n_parentid: 212
    },{
      n_id: 2127,
      n_title: 'Cruise 2021 B',
      code: "cruise_2021_b",
      n_parentid: 212
    },{
      n_id: 2128,
      n_title: 'Cruise 2019 A INALE',
      code: "cruise_2019_a_inale",
      n_parentid: 212
    },{
      n_id: 2129,
      n_title: 'Cruise 2019 B INALE',
      code: "cruise_2019_b_inale",
      n_parentid: 212
    },{
      n_id: 21291,
      n_title: 'Cruise 2021 A INALE',
      code: "cruise_2021_a_inale",
      n_parentid: 212
    },{
      n_id: 21292,
      n_title: 'Cruise 2021 B INALE',
      code: "cruise_2021_b_inale",
      n_parentid: 212
    },{
      n_id: 21293,
      n_title: 'Cruise 2021 C INALE',
      code: "cruise_2021_c_inale",
      n_parentid: 212
    },{
      n_id: 214,
      n_title: 'Marine Natura Sites (Monitored under D1)',
      code: "v_marine_natura2000_end2021_epsg3035_sitetype", //"marine_natura2000_end2021_epsg3035",
      n_parentid: 21
    },{
      n_id: 215,
      n_title: 'EEA Marine Assessment Grid 10x10',
      code: "grid_10km_3035",
      n_parentid: 21
    },{
      n_id: 216,
      n_title: 'EEA Marine Assessment Grid 25x25',
      code: "grid_25km_3035",
      n_parentid: 21
    },{
      n_id: 22,
      n_title: 'OTHER',
      n_parentid: 2,
    }, {
      n_id: 221,
      n_title: 'Poseidon',
      code: "POSEIDON",
      n_parentid: 22
    },{
      n_id: 222,
      n_title: 'Argo',
      code: "argo_stations",
      n_parentid: 22
    },{
      n_id: 223,
      n_title: 'WFD',
      code: "coastal_wfd",
      n_parentid: 22
    },{
      n_id: 3,
      n_title: 'PRODUCTS',
      n_parentid: 0,
    }, {
      n_id: 31,
      n_title: 'MSFD',
      n_parentid: 3,
    }, {
      n_id: 32,
      n_title: 'OTHER',
      n_parentid: 3,
    },{
      n_id: 33,
      n_title: 'WFD',
      n_parentid: 3,
    },{
      n_id: 311,
      n_title: 'D3',
      n_parentid: 31,
    },{
      n_id: 3111,
      n_title: 'Annual Fisheries Production per fishing gear per NSSG area (NSSG: National Statistical Service of Greece)',
      code: 'nssg-annual_prod_per_gear_1990-2019',
      n_parentid: 311,
    },{
      n_id: 3112,
      n_title: 'Annual Fisheries Production per Species per NSSG area (NSSG: National Statistical Service of Greece)',
      code: 'nssg-annual_prod_per_species_1990-2019',
      n_parentid: 311,
    },{
      n_id: 321 ,
      n_title: 'EMODNET Bathymetry',
      code: 'DPTH',
      n_parentid: 32,
      n_hyperlink: "https://doi.org/10.12770/bb6a87dd-e579-4036-abe1-e649cea9881a"
    },{
      n_id: 322 ,
      n_title: 'EMODNET Habitats',
      code: 'HABT',
      n_parentid: 32,
      n_hyperlink: "http://gis.ices.dk/geonetwork/srv/eng/catalog.search#/metadata/10d3d35c-8f8e-40ff-898f-32e0b037356c"
    },
    {
      n_id: 324,
      n_title: 'Probability of coralligenous habitat in the Mediterranean (MEDISEH)',
      code: 'mediseh_cora',
      n_parentid: 32,
      n_hyperlink: "http://gis.ices.dk/geonetwork/srv/eng/catalog.search#/metadata/4da88de5-b0b8-4de4-8aac-99a9b0980736"
    },{
      n_id: 325,
      n_title: 'Probability of maerl habitat in the Mediterranean (MEDISEH)',
      code: 'mediseh_maerl',
      n_parentid: 32,
      n_hyperlink: "http://gis.ices.dk/geonetwork/srv/eng/catalog.search#/metadata/43c7ac30-04da-479d-b5c1-ba621f0981e4"
    },{
      n_id: 326,
      n_title: 'Probability of Posidonia oceanica in the Mediterranean (MEDISEH)',
      code: 'mediseh_posidonia',
      n_parentid: 32,
      n_hyperlink: "http://gis.ices.dk/geonetwork/srv/eng/catalog.search#/metadata/a93cffc8-8f45-47a4-a9bd-c8ffd9ad53fb"
    },{
      n_id: 327 ,
      n_title: 'Seagrass Meadows',
      code: 'greek_seagrass_meadows_v0906_espg3035',
      n_parentid: 32,
      n_hyperlink: "https://www.seanoe.org/data/00765/87740/",
      n_citation: "https://doi.org/10.1515/bot-2022-0011"
    },{
      n_id: 331,
      n_title: 'Integrated Ecological Status',
      code: 'wfd_eco_status_',
      n_parentid: 33
    },{
      n_id: 332,
      n_title: 'Benthic MacroInvertebrates – BMI (D2C1, D5C8, D6C3, D6C5)',
      code: 'wfd_bmi_status_',
      n_parentid: 33
    },{
      n_id: 333,
      n_title: 'Macroalgae (MAI)',
      code: 'wfd_ma_status_',
      n_parentid: 33
    },{
      n_id: 334,
      n_title: 'Angiosperms – AN (D2C1, D6C3, D6C5)',
      code: 'wfd_an_status_',
      n_parentid: 33
    },{
      n_id: 335,
      n_title: 'Chlorophyl-a (D4C2, D5C2)',
      code: 'wfd_chla_status_',
      n_parentid: 33
    },{
      n_id: 336,
      n_title: 'PhysicoChemical Quality Index – PCQI (D5C1, D5C4, D5C5)',
      code: 'wfd_pcqi_status_',
      n_parentid: 33
    },{
      n_id: 337,
      n_title: 'Chemical Status – Chem (D8C1)',
      code: 'wfd_chem_status_',
      n_parentid: 33
    }];

onMounted(() => {
    pTree = new PickleTree({
        c_target: 'layertree', //'maptab_treeview',
        c_config: props.config,
        //   switchCallback: layerTreeSwitch,
          c_data: myData
    });
})
</script>