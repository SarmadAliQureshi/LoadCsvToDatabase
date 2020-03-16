# LoadCsvToDatabase
Reading csv file from local directory and sending to database through POST request.
This code uses papa perser plugin to parse the csv.


<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.1.0/papaparse.js"></script>
<label for="">Upload the product's csv</label>
<input type="file" id="product_csv" name="files"/>

<script>

function handleFileSelectProducts(evt) {
    var file = evt.target.files[0];
    // ...
    console.log(file)
    Papa.parse(file, {
    header: true,
    dynamicTyping: true,
    complete: function(results) {
      data = results;
      dataArray = data['data']
      for (i=0;i<dataArray.length;i++){
          // console.log(dataArray[i])
          // console.log(dataArray[i])
          console.log('newlifne')
          postData = {
          "product_id":dataArray[i].product_id,
          "product_name":dataArray[i].product_description,
          "product_price":dataArray[i].product_price
        } 

        console.log(postData)

          const getUrl = 'http://localhost:3000/product'
          $.ajax({
              url:getUrl,
              type:"POST",
              dataType:"json",
              data:postData
          });
          alert("Products data uploaded")
      }
      // console.log('Data', data)
    }
  });
  }
 
  $(document).ready(function(){
    $("#product_csv").change(handleFileSelectProducts);
  });
</script>
