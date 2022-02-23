<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
        <link rel="stylesheet" href="custom.css">
        <title>Pregnancy Calculator Tool</title>
        <style>
            html,body {height: 100vh;}
        </style>
    </head>
    <body>
        <div class="row h-100 mx-0 align-content-center">
            <div class="col-12">
                <div class="container">
                    <div class="col-lg-8 mx-auto">
                        <h1 class="text-center d-block">Gebelik Hesaplama Aracı</h1>
                        <p class="mb-5 text-center">* Gebelik hesaplaması için SAT (son adet tarihinizin) ilk gününü seçiniz.:</p>
                        <div class="row">
                            <div class="col-sm">
                                <label class="fs-6 d-block mb-1">Gün Seçiniz</label>
                                <select id="day" class="form-control"></select>
                            </div>
                            <div class="col-sm">
                                <label class="fs-6 d-block mb-1">Ay Seçiniz</label>
                                <select id="month" class="form-control"> </select>
                            </div>
                            <div class="col-sm">
                                <label class="fs-6 d-block mb-1">Yıl Seçiniz</label>
                                <select id="year" class="form-control"> </select>
                            </div>
                            <div class="col-12 text-end mt-3">
                                <button id="setDueDate" class="btn btn-success w-100">Hesapla</button>
                            </div>
                        </div>
                        <ul class="result mt-5"> </ul>
                    </div>
                </div>
            </div>
        </div> 
        <script>
            

            const day = document.getElementById("day");
            const year = document.getElementById("year");
            const month = document.getElementById("month");
            const result = document.querySelector(".result");
            const setDueDate = document.getElementById("setDueDate");
            const monthDatas = ["Ocak", "Şubat", "Mart", "Nisan", "Mayıs", "Haziran", "Temmuz", "Ağustos", "Eylül", "Ekim", "Kasım", "Aralık"];
            const today = new Date();
            let babyHoroscope;

            function getHoroscope(horoscopeDay, horoscopeMonth) {
                
                if((horoscopeMonth == 1 && horoscopeDay <= 20) || (horoscopeMonth == 12 && horoscopeDay >=22)) {
                    return "Oğlak";
                } else if ((horoscopeMonth == 1 && horoscopeDay >= 21) || (horoscopeMonth == 2 && horoscopeDay <= 18)) {
                    return "Kova";
                } else if((horoscopeMonth == 2 && horoscopeDay >= 19) || (horoscopeMonth == 3 && horoscopeDay <= 20)) {
                    return "Balık";
                } else if((horoscopeMonth == 3 && horoscopeDay >= 21) || (horoscopeMonth == 4 && horoscopeDay <= 20)) {
                    return "Koç";
                } else if((horoscopeMonth == 4 && horoscopeDay >= 21) || (horoscopeMonth == 5 && horoscopeDay <= 20)) {
                    return "Boğa";
                } else if((horoscopeMonth == 5 && horoscopeDay >= 21) || (horoscopeMonth == 6 && horoscopeDay <= 20)) {
                    return "İkizler";
                } else if((horoscopeMonth == 6 && horoscopeDay >= 22) || (horoscopeMonth == 7 && horoscopeDay <= 22)) {
                    return "Yengeç";
                } else if((horoscopeMonth == 7 && horoscopeDay >= 23) || (horoscopeMonth == 8 && horoscopeDay <= 23)) {
                    return "Aslan";
                } else if((horoscopeMonth == 8 && horoscopeDay >= 24) || (horoscopeMonth == 9 && horoscopeDay <= 23)) {
                    return "Başak";
                } else if((horoscopeMonth == 9 && horoscopeDay >= 24) || (horoscopeMonth == 10 && horoscopeDay <= 23)) {
                    return "Terazi";
                } else if((horoscopeMonth == 10 && horoscopeDay >= 24) || (horoscopeMonth == 11 && horoscopeDay <= 22)) {
                    return "Akrep";
                } else if((horoscopeMonth == 11 && horoscopeDay >= 23) || (horoscopeMonth == 12 && horoscopeDay <= 21)) {
                    return "Yay";
                }
            }
            
            let i = 0;
            let newSelectDate = new Date();
            const yearData = newSelectDate.getFullYear();
            year.innerHTML = "<option value='" + yearData + "'>" + yearData + "</option><option value='" + (yearData - 1) + "'>" + (yearData - 1) + "</option>";

            for (i = 1; i <= 31; i++) {
                day.innerHTML += "<option value='" + i + "'>" + i + "</option>";
            }
            for (i = 1; i <= 12; i++) {
                month.innerHTML += "<option value='" + i + "'>" + monthDatas[i - 1] + "</option>";
            }



            setDueDate.addEventListener("click", function () { 
                
                let horoscopeDate = new Date(formatDate(getStartDate(), "2", 273));

                result.innerHTML = "";
                result.innerHTML += "<li><span>Bebek : </span><strong> " + formatDate(getStartDate(),"1",0) + " </strong></li>";
                result.innerHTML += "<li><span>Cinsiyet belirlenme tarihi : </span><strong> " + formatDate(getStartDate(), "1", 112) + "  </strong></li>";
                result.innerHTML += "<li><span>Tahmini Doğum : </span><strong> " + formatDate(getStartDate(), "1", 273) + " </strong></li>";
                result.innerHTML += "<li><span>Burç : </span><strong> " + getHoroscope(horoscopeDate.getDay(),horoscopeDate.getMonth()) + " </strong></li>";
                result.innerHTML += "<li><span>Muhtemel gebe kalma tarihiniz : </span><strong> " + formatDate(getStartDate(), "1", -14) + " </strong></li>";
                result.innerHTML += "<li><span>İkili test için en iyi tarih aralığı <small class='text-primary'>(12 hafta ila 13 hafta)</small> : </span><strong> " + formatDate(getStartDate(), "1", 87) + ' - ' + formatDate(getStartDate(),"1", 94) + " </strong></li>";
                result.innerHTML += "<li><span>Organ Tarama Ultrasonu (2. düzey ultrason) Tarihi <small class='text-primary'>(20 hafta ila 22 hafta)</small> : </span><strong> " + formatDate(getStartDate(), "1", 140) + ' - ' + formatDate(getStartDate(), "1", 154) + " </strong></li>";
                result.innerHTML += "<li><span>Bebeğinizin İlk Kalp Atışının Ultrasonda Duyulması <small class='text-primary'>(7 hafta ila 8 hafta)</small> : </span><strong> " + formatDate(getStartDate(), "1", 49) + ' - ' + formatDate(getStartDate(), "1", 56) + " </strong></li>";
                result.innerHTML += "<li><span>Risk faktörleri olan hastalarda rahim ağzı uzunluğu değerlendirmek için en iyi zaman : </span><strong> " + formatDate(getStartDate(), "1", 112) + " </strong></li>";
                result.innerHTML += "<li><span>4'lü test için en iyi tarih aralığı <small class='text-primary'>(16 hafta ila 18 hafta)</small>  : </span><strong> " + formatDate(getStartDate(), "1", 112) + ' - ' + formatDate(getStartDate(), "1", 126) + " </strong></li>";
            });

            
            function getStartDate() {
                var startDate = new Date(month.value + "/" + day.value + "/" + year.value);
                return startDate;
            }
            
            function formatDate(date,format = "1", addDays = 0) {
                let formatDate = new Date(date);
                formatDate.setDate(formatDate.getDate() + addDays);
                if(format === "1"){
                    return formatDate.getDate() + " " +  monthDatas[formatDate.getMonth()] + " " + formatDate.getFullYear();
                }else if(format === "2"){
                    return formatDate;
                }
            }

        </script>
    </body>
</html>
