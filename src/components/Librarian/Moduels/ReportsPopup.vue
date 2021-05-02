<template>
    <div id="popup">
        <div id="popup-inner">
            <button id="close-window-button" @click="togglePopup()"> X </button>
            <h2 id="title"> Report </h2>
            <button 
                @click="genereatPdf">
                    Download
            </button>
            <div ref="document">
                Hello There
            </div>
        </div>
    </div>    
</template>

<script>
	import html2pdf from 'html2pdf.js'

export default {

    props: {
        togglePopup: Function
    },

    components: {
    },

    data() {
        return {
            reports: Array
        }
    },

    mounted() {
        this.fetchReports()
    },

    methods: {
        fetchReports: function() {
            this.loaded = false
            fetch('https://blooming-basin-03878.herokuapp.com/library/reports/all')
            .then(res => res.json())
            .then((data) => {
                console.log(data)
                this.reports = data['reports']
                console.log(this.reports)
            })
            .catch(err => console.log(err.message))
        },
        genereatPdf () {
            html2pdf(this.$refs.document, {
                margin: 1,
                filename: 'reports.pdf',
                image: { type: 'jpeg', quality: 0.98 },
                html2canvas: { dpi: 192, letterRendering: true },
                jsPDF: { unit: 'in', format: 'letter', orientation: 'landscape' }
            })
        }
    },
}
</script>

<style scoped>
#popup {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 99;
    background-color: rgba(0, 0, 0, 0.2);

    display: flex;
    align-items: center;
    justify-content: center;
    text-align: left;
}

#popup-inner {
    height: 90%;
    width: 800px;
    background: #FFF;
    border-radius: 10px;
    padding: 18px;
}

#member-details {
    margin-top: 10px;
    margin-bottom: 10px;
    height: 158px;
    width: 100%;
    background: rgb(226, 226, 226);
    border-radius: 10px;
    display: flex;
    flex-wrap: wrap;
    font-size: 20px; 
}

#member-profile-pic {
    margin: 20px;
    width: 110px;
    height: 110px;
    border-radius: 20px;
    background: rgb(153, 153, 153);
    padding: 5px;
}

#info-keys {
    margin-top: 30px;
    color: rgb(99, 99, 99);   

}

#info-values {
    margin-top: 30px;
    margin-left: 20px;
    color: rgb(44, 44, 44);   
}

#book-details {
    margin-top: 10px;
    margin-bottom: 10px;
    height: 215px;
    width: 100%;
    background: rgb(226, 226, 226);
    border-radius: 10px;
    display: flex;
    flex-wrap: wrap;
    font-size: 20px; 
}

#book-pic {
    margin: 20px;
    width: 110px;
    height: 165px;
    border-radius: 10px;
    background: rgb(153, 153, 153);
    padding: 5px;
}


#get-button {
    height: 90%;
    margin-left: 10px;
    background: rgb(24, 151, 255);
    border-radius: 4px;
    color: white;
    font-weight: bold;
    border: none;
    padding-left: 10px;
    padding-right: 10px;
    padding-top: 3px;
    padding-bottom: 3px;
    cursor: pointer;
}

#get-button:disabled {
    background: rgb(143, 143, 143);
    cursor: not-allowed;
}

#get-button:hover:enabled {
    background: rgb(1, 124, 224);
}

#create-member-button {
    width: 100%;
    height: 50px;
    font-weight: bold;
    border: none;
    color: white;
    font-size: 25px;
    border-radius: 10px;
    background: rgb(24, 151, 255);
    justify-content: center;
    cursor: pointer;
}

#update-delete-button-container {
    width: 100%;
    height: 50px;
    justify-content: center;
    display: flex;
    flex-wrap: nowrap;
}

#update-member-button {
    width: 50%;
    height: 50px;
    font-weight: bold;
    border: none;
    color: white;
    font-size: 25px;
    border-radius: 10px;
    background: rgb(24, 151, 255);
    justify-content: left;
    cursor: pointer;
}

#delete-member-button {
    width: 50%;
    height: 50px;
    margin-right: 12px;
    font-weight: bold;
    border: none;
    color: white;
    font-size: 25px;
    border-radius: 10px;
    background: rgb(255, 59, 24);
    justify-content: right;
    cursor: pointer;
}

#create-member-button:disabled {
    background: rgb(143, 143, 143);
    cursor: not-allowed;
}

#create-member-button:hover:enabled {
    background: rgb(1, 124, 224);
}

#close-window-button {
    position: relative;
    float: right;
    background: rgb(253, 65, 65);
	color: white;
    top: -75px;
    border: none;
    right: -5px;
    font-size: 15px;
    border-radius: 5px;
    padding-left: 10px;
    padding-right: 10px;
    padding-top: 5px;
    padding-bottom: 5px;
}

#close-window-button:hover {
    background: rgb(243, 25, 25);
    cursor: pointer;
}

</style>