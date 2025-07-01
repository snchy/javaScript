# javaScript
let title = document.getElementById("title");
let price = document.getElementById("price");
let texes = document.getElementById("texes");
let ads = document.getElementById("ads");
let discount = document.getElementById("discount");
let total = document.getElementById("total");
let count = document.getElementById("count");
let category = document.getElementById("category");
let create = document.getElementById("create");
let Delete_All = document.getElementById('Delete_All')
let SearchTitle = document.getElementById('SearchTitle');
let SearchCategory = document.getElementById('SearchCategory');
let search = document.getElementById('search');


function getTotal() {
    if (price.value>0 ){
        total.innerText= +price.value + +texes.value + +ads.value - +discount.value;
    }else{
        window.alert('The price is not exiistThe price cannot be less than zero, equal to zero, or empty.')
        total.innerText='';
    }
}
let item ; 
function itemArrey(){
    if (localStorage.product != null)
        {
            item = JSON.parse(localStorage.product);
        }else{
            item = [];
        }
};itemArrey()
create.onclick = function savedata(){
    if(count.value == 0 || count.value ==''){
            let opject_item = {
            title : title.value,
            price : price.value,
            texes : texes.value,
            ads : ads.value,
            discount : discount.value,
            count :  count.value,
            category : category.value,
            total : total.innerText
            }
         item.push(opject_item);
        localStorage.setItem('product',JSON.stringify(item));
    }else{
        for (let i=0; i< parseInt(count.value) ; i++){
            let opject_item = {
            title : title.value,
            price : price.value,
            texes : texes.value,
            ads : ads.value,
            discount : discount.value,
            count :  count.value,
            category : category.value,
            total : total.innerText
            }
         item.push(opject_item);
        localStorage.setItem('product',JSON.stringify(item));
         }
    }
    delete_values();
    location.reload();
}
function delete_values(){
    title.value = '';
    price.value = '';
    texes.value = '';
    ads.value = '';
    discount.value = '';
    count.value = '';
    category.value = '';
    total.innerText = '';
}

let tbody = document.getElementById('tbody')
function addTOTable(){
    for (let i=0 ; i<=item.length; i++) {
        tbody.innerHTML += 
            `<tr>
                <th>${i+1}</th>
                <th id="title${i}" >${item[i].title}</th>
                <th id="price${i}" >${item[i].price}</th>
                <th id="texes${i}" >${item[i].texes}</th>
                <th id="ads${i}" >${item[i].ads}</th>
                <th id="discount${i}" >${item[i].discount}</th>
                <th id="total${i}" >${item[i].total}</th>
                <th id="category${i}" >${item[i].category}</th>
                <th onclick = "UpdateITEM(${i})" ><button id="update">UPDATE</button></th>
                <th onclick = "deleteITEM(${i})" ><button id="delete">DELETE</button></th>
            </tr>`
    }
}

function deleteITEM(i){
    item.splice(i,1);
    localStorage.setItem('product',JSON.stringify(item));
    location.reload();
}

function UpdateITEM(i){
    count.style.display = 'none';
    title.value = item[i].title;
    price.value = item[i].price;
    texes.value = item[i].texes;
    ads.value =item[i].ads;
    discount.value = item[i].discount;
    category.value =  item[i].category;
    total.innerText = item[i].total;
    create.outerHTML='<button id="Update">Update</button>';
    let Update = document.getElementById('Update');
    window.scroll({
        behavior: 'smooth', 
        top: 0, 
        left: 0 
    });
    Update.onclick =function(){
        item[i].title = title.value;
        item[i].price = price.value;
        item[i].texes = texes.value;
        item[i].ads = ads.value;
        item[i].discount = discount.value;
        item[i].category = category.value;
        item[i].total = total.innerText;
        localStorage.setItem('product',JSON.stringify(item));
        location.reload();
    }   
}
Delete_All.onclick = function(){
    localStorage.removeItem('product')
    item = [];
    location.reload();
};


SearchTitle.onclick = function(){
    SearchTitle.style.backgroundColor = 'aqua';
    SearchTitle.style.scale = '1.1';
    SearchTitle.style.transition = '2s';
    search.placeholder = 'Search By Title';
    SearchCategory.style.backgroundColor = 'royalblue';
    SearchCategory.style.scale = 'none';
}
SearchCategory.onclick = function(){
    SearchCategory.style.backgroundColor = 'aqua';
    SearchCategory.style.scale = '1.1';
    SearchCategory.style.transition = '2s';
    search.placeholder = 'Search By Category';
    SearchCategory.style.transition = '2s';
    SearchTitle.style.backgroundColor = 'royalblue';
    SearchTitle.style.scale = 'none';
}

search.onkeyup = function(){
    if (search.placeholder=='Search By Title'){
        tbody.innerHTML = '';
        for(let i =0 ; i<item.length ;i++){
            if (item[i].title.includes(search.value)){
                tbody.innerHTML += 
                `<tr>
                    <th>${i+1}</th>
                    <th id="title${i}" >${item[i].title}</th>
                    <th id="price${i}" >${item[i].price}</th>
                    <th id="texes${i}" >${item[i].texes}</th>
                    <th id="ads${i}" >${item[i].ads}</th>
                    <th id="discount${i}" >${item[i].discount}</th>
                    <th id="total${i}" >${item[i].total}</th>
                    <th id="category${i}" >${item[i].category}</th>
                    <th onclick = "UpdateITEM(${i})" ><button id="update">UPDATE</button></th>
                    <th onclick = "deleteITEM(${i})" ><button id="delete">DELETE</button></th>
                </tr>`
            }
        }

     } else if (search.placeholder=='Search By Category') {
        tbody.innerHTML = '';
        for(let i =0 ; i<item.length ;i++){
            if (item[i].category.includes(search.value)){
                tbody.innerHTML += 
                `<tr>
                    <th>${i+1}</th>
                    <th id="title${i}" >${item[i].title}</th>
                    <th id="price${i}" >${item[i].price}</th>
                    <th id="texes${i}" >${item[i].texes}</th>
                    <th id="ads${i}" >${item[i].ads}</th>
                    <th id="discount${i}" >${item[i].discount}</th>
                    <th id="total${i}" >${item[i].total}</th>
                    <th id="category${i}" >${item[i].category}</th>
                    <th onclick = "UpdateITEM(${i})" ><button id="update">UPDATE</button></th>
                    <th onclick = "deleteITEM(${i})" ><button id="delete">DELETE</button></th>
                </tr>`
            }
        }        
    }else {
        alert('enter the type of search')
    }
    
}




addTOTable();
