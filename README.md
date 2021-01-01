# whattotwweet
what to tweet

async function callingFn() {
      try {
          const response = await fetch("https://api.airtable.com/v0/apppWVj7HuPgOxMw7/Table%201?api_key=keyvcM7SZx5SoGl0n", {
              method: "get",
              headers: {
                  "Content-Type": "application/json"
              }
          });
          const json = await response.json();
          return json["records"]
      } catch (error) {
          console.error("Error:", error);
      }
  }
  
get_random = function (list) {
  return list[Math.floor((Math.random()*list.length))];}
  
  (async () => {

    /* call the function that loads data from Airtable and save it in variable called res */
    var res = await callingFn();

	/* define a new function that loads a new random prompt into the corresponding HTML elements */
    async function fetch_new_prompt(results) {
    
    /* pick HTML element with id="idea1". This is the element that shows the prompt */
    const idea1 = document.getElementById('idea1'); 

	/* pick random element from the list results. Below, we call the function we define here with res as the argument which is the variable that contains the Airtable data. */
    const picked_prompt = get_random(results);
		
	/* change the text inside the element we picked above to the new prompt */
    idea1.innerHTML = picked_prompt["fields"]["Prompt"];

    /* change the tweet image and tweet source link elements analogously */
    document.getElementById("tweetimage").src = picked_prompt["fields"]["Example 1"][0]["url"];
    document.getElementById("tweetsource").href = picked_prompt["fields"]["Example 1 Link"];
    }
		
	
	/* We call this function and feed it the data we loaded from Airtable in the previous step as soon as the website is loaded.*/
    $(document).ready(function(){fetch_new_prompt(res)});

	/* We also call this function when the element with id=newprompt gets clicked. */
    $(document).ready(function(){
      $('#newprompt').click(function(){
         fetch_new_prompt(res);
      });
    });

	/* We also call this function when someone presses the space bar. */
    document.body.onkeyup = function(e){
      if(e.keyCode == 32 || e.key === ' '){
          fetch_new_prompt(res);
      }
    }
  })()
  
  function showhide() {

/* pick the HTML element with id="tweetsource". This is the div that contains the tweet image */
  var aelement = document.getElementById("tweetsource");
	
 /* show the element when it's hidden, hide it when it's shown.*/
  aelement.classList.toggle('hidden'); 
	
/* change the text on button from "Show Example" to "Hide Example" and vice versa */
  var examplebutton =  document.getElementById("examplebutton");
  if (examplebutton.innerHTML == "Hide Example") {
      examplebutton.innerHTML = "Show Example";
  } else {
      examplebutton.innerHTML = "Hide Example";
  }

}

<a
	href="#" id="examplebutton" onclick="showhide();"
	class="inline-flex items-center justify-center h-12 px-6 font-medium tracking-wide text-gray-900    focus:outline-none"
>
	Show Example
</a>
