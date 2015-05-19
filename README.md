<!DOCTYPE html>

<head>
<title>JSON Table</title>
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js"></script>
<style>
.shoppingTable h2{
		color:green;
}
.shoppingTable table{
    border: 1px solid #ccc;
}
.shoppingTable table th {
    border-bottom: 1px solid #ccc;
    border-right: 1px solid #ccc;
     padding: 5px 18px;
}
.shoppingTable table td {
    border-bottom: 1px solid #ccc;
    border-right: 1px solid #ccc;
}
</style>


</head>

<body>
<div class="shoppingTable">
	  <h2>Shopping Cart</h2>
   <table id="shoptable">	 
   <tr>
	   <th>ID</th>
       <th>Product Name</th>
       <th>Price</th>
       <th>Quantity</th>
       <th>Description</th>
       <th>Add</th>
   </tr>

   </table>
  
  <h2>My Cart</h2>
   <table id="mycart">	 
   <tr>
	   <th>Product Name</th>
       <th>Price</th>
       <th>Quantity</th>
       <th>Remove</th>
   </tr>

   </table>
  
  
</div>
<script>
var products=[  
      {
         "id":"1",
         "productName":"Mobile",
         "Price":"15000",
         "stock":"10",
         "description":"Dual Sim,Long lasting battery"
      },
      {
         "id":"2",
         "productName":"Watch",
         "Price":"1500",
         "stock":"30",
         "description":"Atractive watches with good offer"
      },
      {
         "id":"3",
         "productName":"Shoes",
         "Price":"200",
         "stock":"0",
         "description":"The best match for your foot"
      }
   ];
var len = products.length;
var i,k;
for(i=0;i<len;i++){
	k=i;
	a=++k;	
 jQuery("table#shoptable").append( '<tr id="'+(i)+'"><td class="product-id">' + products[i].id + '</td> + <td class="product-name">' + products[i].productName + '</td> + <td class="product-price">' + products[i].Price + '</td> + <td class="shoppingproductName" id = "'+ a + products[i].productName +'">' + products[i].stock + '</td> + <td>' + products[i].description + '</td> + <td><button class="addCart">Add to Cart</button></td></tr>');
};
 var m=0;
$('.addCart').click(function(){
	var productqty=$(this).parent().closest('tr').find('.shoppingproductName').text();
	 // alert($(this).parent().closest('tr').find('.shoppingproductName').text());
	 //alert();
	 if(productqty>0){
		 $(this).parent().parent().find('.shoppingproductName').text(productqty-1);
	addtocart($(this).parent().parent().attr('id'),productqty-1);
     } else{
      alert('out of stock');
    }
	
});
$('#mycart').on('click', '.remove', function(){
	removeid=$(this).parent().attr('id');
	removecount=$(this).parent().find('.count').text();
	removecart(removeid,removecount);
});
function addtocart(id,count){
	//alert(id);
	cart_count = products[id].stock - count;
	//cart_count = data.products[id].stock - count;	
	if(cart_count <= 1){
		var tdata_row = $('<tr id="'+id+'"><td>'+products[id].productName+'</td><td>'+products[id].Price+'</td><td class="count">'+cart_count+'</td><td class="remove">Remove</td></tr>');
		tdata_row.appendTo('#mycart');
	}
	else {
		//alert($('#mycart tr#'+id).find('.count').text(cart_count));
		$('#mycart tr#'+id).find('.count').text(cart_count);
	}
	//return true;
}
function removecart(removeid,removecount){
	//alert(removeid);
      $('#mycart tr#'+removeid).find('.count').text(removecount-1);
	cancel_count = products[removeid].stock - (removecount-1);
	$('#shoptable tr#'+removeid).find('.shoppingproductName').text(cancel_count);
	if (removecount == 1) {
		$('#mycart tr#'+removeid).remove();
	}
}

</script>
</body>

</html>
