<template>
</template>

<script>
export default {
    data() {
        return {
            y: '0',
            m: '0'
        }
    },
    props: ['edYM'],
    watch: {
        edYM(a) {
            this.y = a[0]
            this.m = a[1]
            this.getTxt(this.y,this.m)
        }
        //this.y = this.edY
        //this.m = this.edM
        //console.log(this.y)
    },
    methods: {
        getTxt(yyyy,mm) {
            $.ajax({
                url: './src/components/txt/'+yyyy+'/'+mm+'.txt',
                dataType: 'text'
            }).done(this.setCalender);
        },
        setCalender(data) {
            $('table').remove();
            var rawAllDates = data.split(/\r?\n|\r/);
            var allDates = rawAllDates.filter(function(item) {
                return item !== null && item !== undefined && item !== '';
            });
            var table = '<table><thead><tr><th>일</th><th>월</th><th>화</th><th>수</th><th>목</th><th>금</th><th>토</th></tr></thead><tbody>';
            for (var singleDate = 0; singleDate < allDates.length; singleDate++) {
                if (singleDate % 7 === 0) {
                table += '<tr>'
                }
                table += '<td>'
                if (!(allDates[singleDate] == '0')) {
                var schS = allDates[singleDate].split('●');
                for (var sch = 0; sch < schS.length; sch++) {
                    if (sch === 0) {
                    table += '<date>' + schS[0] + '</date>'
                    } else {
                    var rawSch = schS[sch].split('○')
                    table += '<button class="sch"><span class="schTitle">[' + rawSch[0] + ']</span><span class="detail_shown"> ' + rawSch[1] + '</span></button><hv><p class="detail_hidden">' + rawSch[1] + '</p>'
                    if (!(rawSch[2] == '0')) {
                        table += rawSch[2]
                    }
                    if (!(rawSch[3] == '0')) {
                        table += '<p class="mem">' + rawSch[3] + '</p>'
                    }
                    table += '</hv>'
                    }
                }
                }
                table += '</td>'
                if (singleDate % 7 === 6) {
                table += '</tr>'
                }
            }
            table += '</tbody>';
            table += '</table>';
            $('#table').append(table);
        }
    }
}
</script>