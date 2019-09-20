Title: Lecture6 Details
Date: 2019-07-23 23:39
Modified: 2019-05-07 23:39
Category:Module 1

#Topic Nmae: Multi-Layer Perceptrons

#<li><a href="https://drive.google.com/file/d/1Kjk7wyXsU1p_IUbY4WRMK7cH85tcr___/view?usp=sharing" target="_blank">Pre-Reading</a></li> <br>

#Slides<br>
#<li><a href="https://www.dropbox.com/home/Batch7/Slides/Day08?preview=MLP.pptx" target="_blank">Multi-Layer Perceptrons</a></li> <br>

#Preview Video <br><br>
<iframe src="https://videoken.com/embed/vkene-a0yjEjEBKw"width="640" height="480"></iframe>

#Experiments<br><br>
**MLP_MNIST**<br>
1. Understanding Multi-Layer Perceptron (MLP)and tuning the hyper-parameters of a MLP classifier<br>
**Note:**Here is the following Notebook For [MLP_MNIST](https://drive.google.com/file/d/1wlBHSE5DsBUCCsKPpxSuOqvFBfWcDzk7/view?usp=sharing)
<br>
###Experiment Explanation Video <br><br>
<iframe src="https://cdn.talentsprint.com/talentsprint/archives/sc/aiml/aiml_2018_b7_hyd/experiment_details_backup/mlp_mnist.mp4"width="640" height="480"></iframe>

<br>

**MLP_CIFAR10**<br>
1. Understanding CIFAR-10 datasetand experiment using MLP algorithm <br>

**Note:**Here is the following Notebook For [MLP_CIFAR10](https://drive.google.com/file/d/1ndFesZfvE5EWIWClYvs1XrKcsl4f7VS8/view?usp=sharing)
###Experiment Explanation Video <br><br>
<iframe src="https://cdn.talentsprint.com/talentsprint/archives/sc/aiml/aiml_2018_b7_hyd/experiment_details_backup/mlp_cifar.mp4"width="640" height="480"></iframe>

<br>
#Lecture Video (Batch 9) <br><br>
<iframe src="https://videoken.com/embed/vkene-F-yMsinDWw"width="640" height="480"></iframe>



<head>

   	
<meta name="description" content="Use a free Google Firebase Database to allow visitors to leave comments on your web pages. From https://AlanSimpson.me/firebase">      
<meta name="author" content="Alan Simpson">
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta http-equiv="X-UA-Compatible" content="ie=edge">
<!--===============================================================================================-->
	<link rel="icon" type="image/png" href="images/icons/favicon.ico"/>
<!--===============================================================================================-->
	<link rel="stylesheet" type="text/css" href="vendor/bootstrap/css/bootstrap.min.css">
<!--===============================================================================================-->
	<link rel="stylesheet" type="text/css" href="fonts/font-awesome-4.7.0/css/font-awesome.min.css">
<!--===============================================================================================-->
	<link rel="stylesheet" type="text/css" href="vendor/animate/animate.css">
<!--===============================================================================================-->
	<link rel="stylesheet" type="text/css" href="vendor/css-hamburgers/hamburgers.min.css">
<!--===============================================================================================-->
	<link rel="stylesheet" type="text/css" href="vendor/animsition/css/animsition.min.css">
<!--===============================================================================================-->
	<link rel="stylesheet" type="text/css" href="vendor/select2/select2.min.css">
<!--===============================================================================================-->
	<link rel="stylesheet" type="text/css" href="vendor/daterangepicker/daterangepicker.css">
<!--===============================================================================================-->
	<link rel="stylesheet" type="text/css" href="css/util.css">
	<link rel="stylesheet" type="text/css" href="css/main.css">
<!--===============================================================================================-->

<style> 
      
      li#news  {
           width: 500px;
           height: 40px;
           background: #b2beb5;
           border-radius: 5px;
           
        }
</style>


</head>

<body>

<div class="container-contact100" id="allcomments">
 <div class="wrap-contact100">
                      
	<form class="contact100-form validate-form" id = "newcomment">
 

        
       <ul id="lecture6"></ul>


	<span class="contact100-form-title"> Comments Box</span>

	<div class="wrap-input100 validate-input" data-validate="Please enter your name">
       <input class="input100" id="tbName" type="text" maxlength="20" placeholder="Full Name" required>	
        <span class="focus-input100"></span>
	</div>

	<div class="wrap-input100 validate-input" data-validate = "Please enter your comment">
       <textarea  class="input100" id="txComment" maxlength="4096" required style="width:96%" placeholder="Please enter your comment"></textarea>
	<span class="focus-input100"></span>
	</div>
	<button class="contact100-form-btn" id="btnSubmitComment" value="Submit"><span>
	<i class="fa fa-paper-plane-o m-r-6" aria-hidden="true"></i>submit</span>
	</button>
			
     </form>
 </div>
</div>
 
<!-- Connection to Firebase -->
<script src="https://www.gstatic.com/firebasejs/6.4.0/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/6.4.0/firebase-firestore.js"></script>
<script src="https://www.gstatic.com/firebasejs/6.4.0/firebase-database.js"></script>

<script>
    // Your web app's Firebase configuration
var firebaseConfig = {
       apiKey: "AIzaSyAP54I0zA3Z9LccG8A40SavPGWKSWqQIX4",
       authDomain: "comments-box.firebaseapp.com",
       databaseURL: "https://comments-box.firebaseio.com",
       projectId: "comments-box",
       storageBucket: "",
       messagingSenderId: "704881653750",
       appId: "1:704881653750:web:91c534874fcbb716"
     };
      // Initialize Firebase
      firebase.initializeApp(firebaseConfig);

       //Rootref is the whole database.
       const rootRef = firebase.database().ref();
       //commentsRef is just the pageCountsNode
       const commentsRef = rootRef.child('comments/lecture6');
       //Listen for click on Submit Comment button, and post comment.
       document.getElementById("btnSubmitComment").addEventListener("click", function () {
       //Replace line breaks in comment with br tags.
       var newcomment = document.getElementById('txComment').value.replace(/\n/g, "<br>");
       //Define a new, keyed post.
       var newPostRef = commentsRef.push();
       //Fill tne new keyed post with data
       newPostRef.set({
       name: document.getElementById('tbName').value.trim(),
       comment: newcomment.trim(),
       frompage: location.pathname,
       when: firebase.database.ServerValue.TIMESTAMP
       });
     });

       function showpastcomments() {
       var showat = document.getElementById('lecture6');
       //Get comments whose from page equals this page's pathname.
       var commentsRef = firebase.database().ref('comments/lecture6');
       commentsRef.once('value', function (snapshot) {
       snapshot.forEach(function (itemSnapshot) {
       //Get the object for one snapshot
       var itemData = itemSnapshot.val();
       //console.log(Object.keys(itemData))
       //console.log(k);
       var comment = itemData.comment;
       var name = itemData.name;
       var k = itemSnapshot.key;
       var kd = itemSnapshot.val();
       console.log(kd)
       //var key = Object.keys(itemSnapshot.val())[2];
       console.log(k)
       var remove = ' <input type="button"  value="Delete" id = "' +k+'" class="delButton" onclick="removeData_1(this)" />';
       var reply = ' <input type="button"  value="Reply" id = "' +k+'" class="Reply" onclick="reply(this)" />';
       var when = new Date(itemData.when).toLocaleDateString("en-us");
       showat.innerHTML +=  name 
       showat.innerHTML += "<li id='news'>" + comment +"</span>--<span> (" + when +")</span></li>";
       })
     })
  }
    //Called when page first opens and also after Submit button click to show all comments for this page.
       showpastcomments()



    </script>
<script src = "https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.4/jquery.js"></script>
<script>
//
//$(".delButton").on("click", function(){
	
  //let keyvalue =$(this).closest("li").find("span.key").text();
  //let ref = firebase.database().ref('comments/'+ keyvalue);
  
   //ref.child(key).remove();
   //ref.set({})
//});




  
  
</script>

<script>
function removeData_1(params){
   const fb = firebase.database().ref()
   // key = document.getElementById('key').value;
    fb.child('comments/lecture6'+ params.id +'/').remove()
    alert('The comment is deleted successfully!');
    reload_page();
    
   
}
function reload_page(){
   window.location.reload();
  }
  




</script>










