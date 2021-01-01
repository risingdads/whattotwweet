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
  
