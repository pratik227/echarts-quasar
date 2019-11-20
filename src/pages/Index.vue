<template>
  <q-page class="bg-grey-2">
    <q-card class="no-shadow q-pa-sm no-border transparent">
      <q-card-section class="q-pa-none q-ma-none">
        <div class="row">
          <div class="col-6">
            <q-card class="bg-white shadow-11">
              <q-card-section>
                <div class="text-h6 text-grey-8 text-weight-bolder">
                  Bar Chart
                </div>
              </q-card-section>
              <q-card-section class="q-pa-none map_height">
                <IEcharts :option="barChartOption" :resizable="true"/>
              </q-card-section>
            </q-card>
          </div>

          <div class="col-6">
            <q-card class="bg-white q-ml-sm shadow-11">
              <q-card-section>
                <div class="text-h6 text-grey-8 text-weight-bolder">
                  Bar Chart
                  <q-select outlined v-model="selected_product"
                            class="bg-white float-right q-mb-sm " style="width:300px;"
                            :options="product_options" label="Select Product"/>
                </div>
              </q-card-section>
              <q-card-section class="q-pa-none map_height">
                <IEcharts :option="getBarChartOptions" :resizable="true"/>
              </q-card-section>
            </q-card>
          </div>

          <div class="col-6">
            <q-card class="bg-white q-mt-sm shadow-11">
              <q-card-section>
                <div class="text-h6 text-grey-8 text-weight-bolder">
                  Scatter Plot
                </div>
              </q-card-section>
              <q-card-section class="q-pa-none map_height">
                <IEcharts :option="getScatterChartOptions" :resizable="true"/>
              </q-card-section>
            </q-card>
          </div>

          <div class="col-6">
            <q-card class="bg-white q-mt-sm q-ml-sm shadow-11">
              <q-card-section>
                <div class="text-h6 text-grey-8 text-weight-bolder">
                  Scatter Plot (Best Fit Line)
                </div>
              </q-card-section>
              <q-card-section class="q-pa-none map_height">
                <IEcharts :option="getScatterChartOptionsFitLine" :resizable="true"/>
              </q-card-section>
            </q-card>
          </div>

          <div class="col-6">
            <q-card class="bg-white q-mt-sm shadow-11">
              <q-card-section>
                <div class="text-h6 text-grey-8 text-weight-bolder">
                  Pie Chart
                </div>
              </q-card-section>
              <q-card-section class="q-pa-none map_height">
                <IEcharts :option="pieChartOption" :resizable="true"/>
              </q-card-section>
            </q-card>
          </div>

          <div class="col-6">
            <q-card class="bg-white q-ml-sm q-mt-sm shadow-11">
              <q-card-section>
                <div class="text-h6 text-grey-8 text-weight-bolder">
                  Line Chart
                </div>
              </q-card-section>
              <q-card-section class="q-pa-none map_height">
                <IEcharts :option="lineChartOption" :resizable="true"/>
              </q-card-section>
            </q-card>
          </div>

          <div class="col-6">
            <q-card class="bg-white q-mt-sm shadow-11">
              <q-card-section>
                <div class="text-h6 text-grey-8 text-weight-bolder">
                  Stack Bar Chart
                </div>
              </q-card-section>
              <q-card-section class="q-pa-none map_height">
                <IEcharts :option="getStackBarChartOptions" :resizable="true"/>
              </q-card-section>
            </q-card>
          </div>

          <div class="col-6">
            <q-card class="bg-white q-ml-sm q-mt-sm shadow-11">
              <q-card-section>
                <div class="text-h6 text-grey-8 text-weight-bolder">
                  Pie Chart
                </div>
              </q-card-section>
              <q-card-section class="q-pa-none map_height">
                <IEcharts :option="GetPie2Options" :resizable="true"/>
              </q-card-section>
            </q-card>
          </div>

        </div>
      </q-card-section>
    </q-card>
  </q-page>
</template>
<script>
    import IEcharts from 'vue-echarts-v3/src/full.js';
    import numeral from 'numeral'

    export default {
        name: "charts",
        data() {
            return {
                selected_product: 'Matcha Latte',
                data: [
                    {product: 'Matcha Latte', '2015': 43.3, '2016': 85.8, '2017': 93.7},
                    {product: 'Milk Tea', '2015': 83.1, '2016': 73.4, '2017': 55.1},
                    {product: 'Cheese Cocoa', '2015': 86.4, '2016': 65.2, '2017': 82.5},
                    {product: 'Walnut Brownie', '2015': 72.4, '2016': 53.9, '2017': 39.1}
                ],
                product_options: ['Matcha Latte', 'Milk Tea', 'Cheese Cocoa', 'Walnut Brownie'],
                barChartOption: {
                    grid: {
                        bottom: '25%'
                    },
                    legend: {},
                    tooltip: {},
                    dataset: {
                        dimensions: ['product', '2015', '2016', '2017'],
                        source: [
                            {product: 'Matcha Latte', '2015': 43.3, '2016': 85.8, '2017': 93.7},
                            {product: 'Milk Tea', '2015': 83.1, '2016': 73.4, '2017': 55.1},
                            {product: 'Cheese Cocoa', '2015': 86.4, '2016': 65.2, '2017': 82.5},
                            {product: 'Walnut Brownie', '2015': 72.4, '2016': 53.9, '2017': 39.1}
                        ]
                    },
                    xAxis: {
                        type: 'category',
                        axisLabel: {
                            rotate: 45
                        }
                    },
                    yAxis: {},
                    // Declare several bar series, each will be mapped
                    // to a column of dataset.source by default.
                    series: [
                        {type: 'bar'},
                        {type: 'bar'},
                        {type: 'bar'}
                    ]
                },
                lineChartOption: {
                    xAxis: {
                        type: 'category',
                        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
                    },
                    yAxis: {
                        type: 'value'
                    },
                    series: [{
                        data: [820, 932, 901, 934, 1290, 1330, 1320],
                        type: 'line'
                    }]
                },
                scatter_data: [
                    [18.78, 22365], [49.26, 18271], [70.58, 20545], [75.67, 21806], [108.88, 19747], [123.31, 19464], [173.62, 16704], [206.54, 22272], [222.57, 22016], [278.52, 21543], [293.35, 22158], [310.46, 18038], [18.06, 25471], [53.06, 24878], [60.03, 24988], [86.35, 28373], [96.01, 27081], [122.11, 29482], [139.06, 28046], [160.23, 28709], [173.2, 26559], [192.45, 25877], [213.91, 28985], [237.83, 25649], [251.01, 24701], [294.77, 26801], [321.42, 28623], [368.52, 25779], [35.98, 34742], [51.11, 35219], [60.59, 34660], [93, 31721], [102.55, 35983], [114.76, 36250], [137.57, 36709], [159.87, 35029], [175.44, 33630], [194.76, 35942], [211.19, 35514], [235.4, 29737], [259.57, 36599], [273.19, 36166], [292.21, 31827], [314.01, 36624], [33.08, 43834], [49.68, 41265], [56.44, 40575], [89.91, 43600], [99.32, 38261], [124.73, 40087], [135.86, 41955], [160.24, 39004], [174.93, 40017], [191.01, 37747], [212.21, 42411], [239.96, 40007], [263.43, 37961], [272.85, 39216], [301.94, 42393], [306.66, 42393], [325.1, 38143], [367.31, 40293], [35.51, 50127], [52.56, 50419], [58.13, 44728], [87.47, 45730], [98.15, 45849], [119.63, 50155], [133.74, 48602], [158.83, 49739], [189.34, 44893], [195.8, 44434], [221.8, 47340], [241.67, 44690], [262.83, 49462], [274.51, 49179], [286.43, 48878], [327.27, 44306], [353.44, 45836], [32.18, 55000], [52.88, 55787], [63.18, 56189], [80.13, 53663], [98.23, 57010], [115.28, 55518], [147.18, 51502], [164.67, 54655], [184.44, 56930], [207.48, 55428], [209.73, 57217], [244.19, 53156], [252.61, 53838], [289.45, 55278], [304.91, 55755], [324.98, 52311], [390.44, 56347], [29.23, 62950], [45.64, 60912], [59.38, 61806], [83.05, 59603], [98.64, 59915], [119, 59412], [144.8, 59807], [164.17, 59999], [180.93, 60797], [192.1, 65591], [214.02, 59808], [242.89, 63815], [257.83, 62057], [271.32, 64500], [286.26, 59387], [311.95, 58664], [349.71, 65769], [367.19, 62638], [36.86, 69452], [43.12, 66095], [59.45, 68630], [84.07, 71370], [101.94, 70140], [127.82, 72759], [145.86, 68559], [158.42, 71645], [173.48, 69980], [204.47, 68470], [222.08, 69795], [238.05, 71414], [260.91, 70906], [281.02, 69391], [291.24, 68672], [310.35, 69599], [33.48, 74373], [47.54, 79933], [72.49, 76977], [93.86, 73301], [107.5, 77210], [129.64, 77137], [147.24, 73350], [169.6, 79953], [184.3, 73251], [190.32, 79866], [222.65, 77701], [238.03, 74781], [249.33, 80135], [270.93, 75666], [297.51, 73275], [305.37, 74991], [335.85, 77416], [357.76, 74911], [399.48, 75098], [35.81, 82380], [55, 80910], [67.59, 84924], [79.54, 82349], [107.81, 83481], [119.41, 82489], [151.18, 85991], [155.47, 84904], [185.05, 83762], [192.52, 80512], [225.74, 86383], [227.94, 85023], [247.11, 82960], [298.79, 86951], [26.86, 91214], [53.89, 90926], [73.9, 87957], [85.9, 92550], [103.41, 93802], [115.76, 90705], [145.83, 89008], [153.23, 93977], [186.99, 93588], [198.95, 90475], [217.24, 89763], [245.3, 89687], [250.97, 87660], [284.43, 91411], [292.03, 89032], [319.89, 89406], [36.8, 99185], [54.21, 97768], [62.78, 94935], [86.12, 95216], [101.93, 98107], [124.27, 99783], [132.71, 101726], [155, 100000], [179.03, 98308], [192.16, 94973], [223.79, 98307], [241.28, 95325], [259.25, 96433], [266.66, 97503], [303.43, 95574], [306.4, 101175], [324.22, 98699], [28.65, 106458], [43.96, 106688], [58.77, 105156], [81.2, 104065], [106.33, 103452], [124.69, 108269], [138.94, 105082], [158.6, 102144], [178.6, 105824], [194.48, 105358], [211.1, 104217], [234.89, 108562], [266.01, 105260], [290.69, 106643], [314.28, 108184], [398.61, 107624], [28.65, 109948], [54.26, 110579], [60.66, 113749], [82.1, 110232], [102.98, 111673], [126.4, 113133], [133.95, 111983], [160.47, 109990], [172.75, 113459], [200.19, 114891], [218.46, 114438], [246.32, 109573], [275.71, 111712], [287.7, 116441], [25.52, 118731], [44.5, 116854], [72.52, 116934], [77.7, 119692], [109.51, 123277], [116.43, 118527], [139.27, 119911], [169.35, 118099], [173.25, 121213], [200.35, 117295], [218.81, 121110], [238.51, 117396], [261.19, 118688], [284.62, 119458], [295.62, 118396], [310.17, 122514], [330.86, 119386], [34.22, 129457], [46.23, 124811], [74.35, 124950], [83.51, 124536], [100.61, 129212], [128.56, 126012], [146.36, 129817], [165.64, 129800], [176, 124148], [193.21, 129963], [221.56, 126377], [230.75, 130011], [255.52, 129149], [283.6, 129937], [295.56, 128570], [305.54, 130916], [336.9, 129000], [31.2, 134936], [56.2, 135232], [72.38, 131252], [80.8, 134901], [111.7, 133394], [119.21, 132540], [133.72, 134610], [151.82, 131735], [187.86, 133078], [198.63, 133414], [210.01, 133327], [234.12, 136683], [247.9, 133119], [275.99, 137687], [286.01, 132863], [25.94, 142637], [54.17, 143992], [67.5, 139260], [83.9, 144220], [104.44, 142666], [131.88, 144071], [139.21, 143525], [164.22, 138839], [182.57, 142959], [191.81, 144988], [226.84, 141069], [232.19, 139972], [248.08, 141084], [289.65, 139997], [38.4, 151042], [66.2, 149547], [93.4, 147752], [95.98, 147948], [114.93, 147917], [136.35, 152549], [156.73, 148664], [172.31, 149731], [191.69, 148000], [235, 148937], [27.38, 155223], [39.8, 153267], [62.27, 159949], [82.2, 158151], [106.27, 159970], [119.33, 159977], [149.22, 154135], [175.51, 159536], [198.09, 159978], [136.08, 159980], [53.37, 22110], [57.37, 21789], [81.39, 20642], [110.21, 20870], [117.78, 18679], [190.77, 15202], [18.78, 23430], [42.64, 23453], [58.96, 27138], [89.63, 29009], [102.57, 29249], [129.18, 28643], [150.28, 28614], [164.1, 29556], [185.53, 25279], [191.17, 28771], [213.38, 24956], [241.1, 27085], [289.01, 24913], [321.42, 28623], [35.19, 34954], [54.4, 31250], [56.24, 35562], [92.85, 32311], [104.85, 34812], [131.9, 31464], [141.37, 33105], [153.16, 34278], [171.43, 35292], [206.06, 35670], [210.97, 31190], [233.64, 36381], [260.61, 35609], [266.63, 33755], [291.27, 34333], [320.1, 34990], [36.78, 38880], [53.98, 37978], [56.35, 43479], [88.22, 38541], [97.09, 41199], [119.91, 38780], [143.34, 36976], [154.73, 39941], [172.65, 40545], [192.18, 41628], [217.54, 41372], [234.2, 38002], [251.29, 37805], [275.08, 39989], [301.94, 42393], [32.95, 45524], [52.85, 44466], [56.34, 47924], [86.59, 51392], [106.42, 45105], [130.24, 47989], [143.07, 46132], [160.47, 48296], [184.37, 47188], [199.8, 45046], [220.32, 45389], [229.5, 48802], [248.93, 49613], [280.03, 49995], [298.02, 45299], [326.15, 49058], [32.9, 57751], [45.4, 58371], [57.59, 55566], [88.73, 52970], [96.22, 56122], [124.09, 52785], [143.65, 52211], [165.2, 56296], [174.99, 56004], [197.32, 55748], [212.81, 56389], [228.71, 56404], [265.55, 55734], [289.45, 55278], [316.68, 52104], [33.31, 64546], [46.24, 59040], [73.27, 60871], [90.97, 60460], [102.62, 60418], [121.03, 64943], [143.92, 61146], [154.62, 61441], [184.07, 62477], [192.32, 61877], [210.19, 64228], [228.28, 60453], [254.97, 61498], [269.27, 61277], [295.27, 59268], [311.95, 58664], [36.69, 69774], [45.18, 68615], [64.73, 72610], [91.18, 71288], [106.87, 67934], [128.68, 66056], [148.61, 72001], [158.6, 69988], [180.42, 72055], [193.47, 69779], [218.36, 66405], [237.2, 70827], [263.27, 68371], [269.88, 68549], [288.75, 66840], [36.76, 74810], [41.26, 79739], [64.12, 79851], [77.16, 77761], [112.67, 78992], [129.04, 75946], [135.26, 77998], [151.72, 74480], [185.96, 80125], [189.85, 74796], [224.95, 80018], [232.47, 75279], [249.27, 78630], [267.44, 74784], [335.67, 73883], [33.52, 86516], [52.37, 81154], [63.24, 80488], [90.32, 86360], [98.32, 87470], [117.87, 83991], [148.51, 82015], [164.9, 83688], [171.98, 87220], [198.13, 80756], [213.63, 82386], [240.78, 82233], [257.4, 85471], [286.26, 83840], [36.5, 94521], [50.3, 94434], [56.43, 90378], [85.89, 89650], [98.43, 91436], [127.95, 93787], [134.81, 89979], [158.31, 89698], [187.69, 93239], [190.65, 91792], [217.24, 89763], [233.06, 90020], [261.35, 89918], [277.62, 93221], [296.18, 88798], [33.1, 94865], [51.93, 102061], [62.99, 94936], [76.9, 94929], [111.1, 99010], [115.63, 99456], [142.83, 94869], [154.91, 96831], [175.48, 96878], [197.09, 101477], [216.84, 96846], [228.34, 95472], [259.74, 100101], [267.21, 95057], [286.87, 97606], [306.82, 97778], [32.58, 102824], [51.14, 106571], [62.5, 108480], [79.98, 105027], [105.21, 109306], [115.79, 108818], [134.92, 106730], [157.02, 105083], [184.8, 105520], [200.66, 104655], [227.34, 103370], [238.07, 107112], [276.73, 104796], [303.06, 102290], [307.68, 107255], [35.1, 113961], [54.4, 114890], [69.63, 109867], [86.99, 109898], [100.11, 115873], [113.57, 112706], [136.99, 115337], [156.75, 109729], [176.82, 115938], [191.08, 112519], [226.78, 110000], [234.89, 113245], [278.01, 114996], [32.54, 122926], [50.3, 119285], [69.58, 122162], [85.19, 120907], [99.26, 119988], [115.6, 117561], [148.01, 123641], [156.75, 119937], [188.26, 116860], [200.81, 117027], [227.45, 118708], [242.89, 121455], [304.08, 118390], [321.05, 119920], [31.9, 126960], [47, 127660], [60.03, 125771], [75.34, 130077], [102.7, 126388], [121.2, 127888], [139.36, 126149], [163.28, 128614], [175.59, 125235], [193.92, 128920], [232.47, 129049], [314.28, 128866], [28.52, 131487], [52.7, 132828], [59, 132204], [85.72, 131825], [112.7, 133097], [127.38, 133459], [140.33, 132545], [157.58, 136439], [199.4, 135407], [211.29, 136306], [247.83, 136384], [282.92, 134314], [53.2, 144737], [57.4, 139199], [77.5, 144517], [113.21, 140447], [128.3, 138738], [142.1, 142858], [156.2, 138285], [189.9, 139969], [218.81, 143961], [47.66, 145825], [57.6, 149306], [89.28, 146730], [97.97, 148005], [124.3, 146420], [148.55, 146752], [156.98, 146516], [193.98, 149500], [44.3, 153499], [64.96, 153941], [88.62, 154593], [129.1, 153370], [146.42, 159746], [204.6, 159825], [54.24, 22124], [71.1, 20816], [81.39, 21993], [44.2, 26019], [57.67, 26011], [85.34, 28709], [110.16, 24510], [120.89, 28952], [149.38, 28786], [156.72, 27438], [172.26, 24382], [198.68, 28690], [219.19, 24956], [245.19, 28550], [289.01, 24913], [306.87, 25418], [35.39, 36734], [39.85, 30113], [63.63, 31118], [84.21, 32063], [104.85, 33477], [113.75, 35165], [149.6, 34091], [153.69, 32534], [183.49, 29975], [208.29, 36728], [216.03, 31478], [243.33, 34932], [256.04, 32417], [275.62, 34468], [27.1, 42436], [52.53, 43785], [74.58, 40226], [83.16, 41848], [96.77, 43402], [115.39, 39692], [138.49, 40942], [156.49, 38342], [184.64, 37100], [199.59, 39081], [226.98, 44057], [242.68, 39147], [251.29, 38601], [266.59, 37511], [49.07, 46872], [62.83, 46953], [86.6, 49654], [107.22, 49991], [119.54, 50862], [148.34, 46178], [158.7, 49780], [184.37, 47188], [195.49, 46039], [220.32, 45389], [235.23, 47996], [253.4, 50000], [282.02, 49642], [292.56, 45119], [35.49, 52128], [48.67, 54860], [74.94, 58447], [90.4, 56416], [101.78, 57969], [117.72, 57765], [140.6, 52276], [162.44, 54174]]
            }
        },
        methods: {
            onItemClick() {
                // console.log('Clicked on an Item')
            },
            findLineByLeastSquaresMethod(values_x, values_y) {
                var x_sum = 0;
                var y_sum = 0;
                var xy_sum = 0;
                var xx_sum = 0;
                var count = 0;

                /*
                 * The above is just for quick access, makes the program faster
                 */
                var x = 0;
                var y = 0;
                var values_length = values_x.length;

                if (values_length != values_y.length) {
                    throw new Error('The parameters values_x and values_y need to have same size!');
                }

                /*
                 * Above and below cover edge cases
                 */
                if (values_length === 0) {
                    return [[], []];
                }

                /*
                 * Calculate the sum for each of the parts necessary.
                 */
                for (let i = 0; i < values_length; i++) {
                    x = values_x[i];
                    y = values_y[i];
                    x_sum += x;
                    y_sum += y;
                    xx_sum += x * x;
                    xy_sum += x * y;
                    count++;
                }

                /*
                 * Calculate m and b for the line equation:
                 * y = x * m + b
                 */
                var m = (count * xy_sum - x_sum * y_sum) / (count * xx_sum - x_sum * x_sum);
                var b = (y_sum / count) - (m * x_sum) / count;

                /*
                 * We then return the x and y data points according to our fit
                 */
                var result_values = [];

                x = Math.max(...values_x);
                y = x * m + b;
                result_values.push([x, y]);
                x = Math.min(...values_x);
                y = x * m + b;
                result_values.push([x, y]);


                return result_values
                // };
            },
            number_formatter: function (input) {
                if (input)
                    return numeral(input).format('0,0');
                else
                    return input;
            }
        },
        components: {
            IEcharts
        },
        computed: {
            getBarChartOptions() {

                let self = this;

                let filtered_data = this.data.filter(function (item) {
                    return item['product'] == self.selected_product;
                });

                return {

                    grid: {
                        bottom: '25%'
                    },
                    xAxis: {
                        type: 'category',
                        axisLabel: {},
                        nameLocation: "middle",
                        nameGap: 78,
                    },
                    tooltip: {},
                    dataset: {
                        dimensions: ['product', '2015', '2016', '2017'],
                        source: filtered_data
                    },
                    yAxis: {
                        type: 'value',
                        splitLine: {
                            show: false
                        }
                    }, series: [
                        {type: 'bar'},
                        {type: 'bar'},
                        {type: 'bar'}
                    ]
                }
            },
            getScatterChartOptionsFitLine() {


                // scatter_data : [ [18.78, 22365], [49.26, 18271], [70.58, 20545], ....... etc.]

                let values_x_temp = this.scatter_data.map(function (item) {
                    return item[0];
                });
                let values_y_temp = this.scatter_data.map(function (item) {
                    return item[1];
                });

                let val = this.findLineByLeastSquaresMethod(values_x_temp, values_y_temp)

                let self = this;

                return {
                    title: {text: ""},
                    tooltip: {
                        show: true,
                        trigger: "item",
                        formatter: function (param) {
                            return "<span>price-area</span><br />X : " + numeral(param.value[0]).format('0,0') + "% <br />Y  : " + numeral(param.value[1]).format('0,0.00');
                        }
                    },
                    xAxis: {
                        scale: true,
                        nameLocation: "middle",
                        nameGap: 37,
                        axisLabel: {
                            formatter: function (value) {
                                return numeral(value).format('0,0') + '%';
                            }
                        }
                        // splitLine:{
                        //     show:false
                        // }
                        // splitLine: {show: false}
                    },
                    yAxis: {
                        scale: true,
                        nameLocation: "middle",
                        nameGap: 50,
                        axisLabel: {
                            formatter: function (param) {
                                return numeral(param).format('$0a').toUpperCase();
                            }
                        }
                        // splitLine:{
                        //     show:false
                        // }
                    },
                    grid: {left: "15%", bottom: "20%", top: '2%'},
                    series: [
                        {
                            type: "scatter",
                            data: self.scatter_data,
                            symbolSize: 8,
                            itemStyle: {color: "#2f4554"}
                        },
                        {
                            name: "line",
                            type: "line",
                            showSymbol: true,
                            smooth: true,
                            data: val,
                            lineStyle: {type: "dotted"},
                            label: {
                                show: true,
                                formatter: "",
                                textStyle: {align: "right", fontSize: 15},
                                position: "bottom"
                            },
                            silent: true
                        }
                    ]
                }
            },
            getScatterChartOptions() {
                let self = this;
                return {
                    title: {text: ""},
                    tooltip: {
                        show: true,
                        trigger: "item",
                        formatter: function (param) {
                            return "<span>price-area</span><br />X : " + self.number_formatter(param.value[0]) + "% <br />Y  : " + numeral(param.value[1]).format('0,0.00');
                        }
                    },
                    xAxis: {
                        scale: true,
                        nameLocation: "middle",
                        nameGap: 37,
                        axisLabel: {
                            formatter: function (value) {
                                return self.number_formatter(value) + '%';
                            }
                        }
                    },
                    yAxis: {
                        scale: true,
                        nameLocation: "middle",
                        nameGap: 50,
                        axisLabel: {
                            formatter: function (param) {
                                return numeral(param).format('$0a').toUpperCase();
                            }
                        }
                    },
                    grid: {left: "15%", bottom: "20%", top: '2%'},
                    series: [
                        {
                            type: "scatter",
                            data: this.scatter_data,
                            symbolSize: 8,
                            itemStyle: {color: "#2f4554"}
                        }
                    ]
                }
            },
            pieChartOption() {
                return {
                    title: {
                        text: 'Product Pie Chart',
                        x: 'center'
                    },
                    tooltip: {
                        trigger: 'item',
                        formatter: "{a} <br/>{b} : {c} ({d}%)"
                    },
                    legend: {
                        orient: 'vertical',
                        left: 'right',
                        data: ['Prod1', 'Prod 2', 'Prod 3', 'Prod 4', 'Prod 5']
                    },
                    series: [
                        {
                            name: 'Products',
                            type: 'pie',
                            radius: '55%',
                            center: ['50%', '50%'],
                            data: [
                                {value: 335, name: 'Prod 1'},
                                {value: 310, name: 'Prod 2'},
                                {value: 234, name: 'Prod 3'},
                                {value: 135, name: 'Prod 4'},
                                {value: 1548, name: 'Prod 5'}
                            ],
                            itemStyle: {
                                emphasis: {
                                    shadowBlur: 10,
                                    shadowOffsetX: 0,
                                    shadowColor: 'rgba(0, 0, 0, 0.5)'
                                }
                            }
                        }
                    ]
                }
            },
            getStackBarChartOptions() {
                return {
                    tooltip: {
                        trigger: 'axis',
                        axisPointer: {
                            type: 'shadow'
                        }
                    },
                    legend: {
                        data: ['Prod 1', 'Prod 2', 'Prod 3', 'Prod 4', 'Prod 5'],
                        bottom:20
                    },
                    grid: {
                        left: '3%',
                        right: '4%',
                        bottom: '20%',
                        top:'5%',
                        containLabel: true
                    },
                    xAxis: {
                        type: 'value'
                    },
                    yAxis: {
                        type: 'category',
                        data: ['Dataset 1', 'Dataset 2', 'Dataset 3', 'Dataset 4']
                    },
                    series: [
                        {
                            name: 'Prod 1',
                            type: 'bar',
                            stack: 'ad',
                            label: {
                                normal: {
                                    show: true,
                                    position: 'insideRight'
                                }
                            },
                            data: [320, 302, 301, 334]
                        },
                        {
                            name: 'Prod 2',
                            type: 'bar',
                            stack: 'ad',
                            label: {
                                normal: {
                                    show: true,
                                    position: 'insideRight'
                                }
                            },
                            data: [120, 132, 101, 134]
                        },
                        {
                            name: 'Prod 3',
                            type: 'bar',
                            stack: 'ad',
                            label: {
                                normal: {
                                    show: true,
                                    position: 'insideRight'
                                }
                            },
                            data: [220, 182, 191, 234]
                        },
                        {
                            name: 'Prod 4',
                            type: 'bar',
                            stack: 'ad',
                            label: {
                                normal: {
                                    show: true,
                                    position: 'insideRight'
                                }
                            },
                            data: [150, 212, 201, 154]
                        },
                        {
                            name: 'Prod 5',
                            type: 'bar',
                            stack: 'ad',
                            label: {
                                normal: {
                                    show: true,
                                    position: 'insideRight'
                                }
                            },
                            data: [820, 832, 901, 934]
                        }
                    ]
                }
            },
            GetPie2Options() {
                return {
                    tooltip: {
                        trigger: 'item',
                        formatter: "{a} <br/>{b}: {c} ({d}%)"
                    },
                    legend: {
                        orient: 'vertical',
                        x: 'left',
                        data: ['Direct', 'Marketing Advertising', 'Search Engine', 'Mail Marketing', 'Union Advertising', 'Video Advertising', 'Google', 'Bing', 'Other']
                    },
                    series: [
                        {
                            name: 'Access source',
                            type: 'pie',
                            selectedMode: 'single',
                            radius: [0, '30%'],

                            label: {
                                normal: {
                                    position: 'inner'
                                }
                            },
                            labelLine: {
                                normal: {
                                    show: false
                                }
                            },
                            data: [
                                {value: 335, name: 'direct', selected: true},
                                {value: 679, name: 'Marketing Advertising'},
                                {value: 1548, name: 'search engine'}
                            ]
                        },
                        {
                            name: 'Access source',
                            type: 'pie',
                            radius: ['40%', '55%'],
                            label: {
                                normal: {
                                    formatter: '{a|{a}}{abg|}\n{hr|}\n  {b|{b}：}{c}  {per|{d}%}  ',
                                    backgroundColor: '#eee',
                                    borderColor: '#aaa',
                                    borderWidth: 1,
                                    borderRadius: 4,
                                    // shadowBlur:3,
                                    // shadowOffsetX: 2,
                                    // shadowOffsetY: 2,
                                    // shadowColor: '#999',
                                    // padding: [0, 7],
                                    rich: {
                                        a: {
                                            color: '#999',
                                            lineHeight: 22,
                                            align: 'center'
                                        },
                                        // abg: {
                                        //     backgroundColor: '#333',
                                        //     width: '100%',
                                        //     align: 'right',
                                        //     height: 22,
                                        //     borderRadius: [4, 4, 0, 0]
                                        // },
                                        hr: {
                                            borderColor: '#aaa',
                                            width: '100%',
                                            borderWidth: 0.5,
                                            height: 0
                                        },
                                        b: {
                                            fontSize: 16,
                                            lineHeight: 33
                                        },
                                        per: {
                                            color: '#eee',
                                            backgroundColor: '#334455',
                                            padding: [2, 4],
                                            borderRadius: 2
                                        }
                                    }
                                }
                            },
                            data:
                                [
                                    {value: 335, name: 'direct'},
                                    {value: 310, name: 'mail marketing'},
                                    {value: 234, name: 'Union ad'},
                                    {value: 135, name: 'video ad'},
                                    {value: 251, name: 'Google'},
                                    {value: 147, name: 'Bing'},
                                    {value: 102, name: 'Other'}
                                ]
                        }
                    ]
                }
            }
        }
    }
</script>
<style scoped>

  .map_height {
    height: 398px;
  }

</style>
