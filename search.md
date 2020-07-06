---
layout: default
---

<head>
    <link rel="stylesheet" href="{{ "/css/search.css" | prepend: site.baseurl | replace: '//', '/' }}">
</head>

<div class="search">
    <h3>Stand on the shoulders of giants</h3>
    <form>
        <input type="search" placeholder="Search Blog" id="search-input" autofocus autocomplete="off">
        <button type="button" onclick="loadData()">
            <svg focusable="false" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                <path d="M15.5 14h-.79l-.28-.27A6.471 6.471 0 0 0 16 9.5 6.5 6.5 0 1 0 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z">
                </path>
            </svg>
        </button>
        <ul id="results-container"></ul>
    </form>
</div>

<script src="/js/simple-jekyll-search.min.js"></script>
<script>
    function fuzzyQuery(list, keyWord) {
        var reg = new RegExp(keyWord);
        var arr = [];
        for (var i = 0; i < list.length; i++) {
            if (reg.test(list[i])) {
                arr.push(list[i]);
            }
        }
        return arr;
    };
    function isNull( str ){
        if ( str == "" ) return true;
        var regu = "^[ ]+$";
        var re = new RegExp(regu);
        return re.test(str);
    };
    function loadData() {
        if (!searchValue){
            var searchValue = document.getElementById("search-input").value;
            var url = "/js/iresearchbook-100.json"
            var request = new XMLHttpRequest();
            request.open("get", url);
            request.send(null);
            request.onload = function () {
                if (request.status == 200) {
                    var json = JSON.parse(request.responseText);
                    var nameENG = []
                    for(var i=0;i<json['books'].length;i++){
                        nameENG.push(json['books'][i].nameENG);
                    }
                    var queryResult = fuzzyQuery(nameENG, searchValue)
                    if (queryResult.length>0){
                        for(var j=0;j<queryResult.length;j++){
                            console.log(queryResult[j]);
                        }
                    }
                }
            }
        }
    }
</script>
<script>
    var sjs = SimpleJekyllSearch({
        searchInput: document.getElementById('search-input'),
        resultsContainer: document.getElementById('results-container'),
        json: '/search.json'
    })
</script>