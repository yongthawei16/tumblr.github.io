let imageContainer = document.getElementById("image-container");
    let buttons = document.getElementById("button-container");
    let winState = document.getElementById("win-state");
    let resetButton = document.getElementById('reset');

    const apiKey = "9bXA25pPMJ5lpJHIEXaEdp2AnPQQTVYVcveJGyb1rJ2qnM7mhF";
      
    function startGame() {

        //reset
        imageContainer.innerHTML = '';
        buttons.innerHTML = '';
        winState.innerHTML = '';

        // create array && shuffle
        let tagName = ['fashion','automotive','marvel','scenery'];
        tagName = Shuffle(tagName);

        //Get random correct answer
        let randomTag = tagName[Math.floor(Math.random() * tagName.length)];
        let inPlay = true;
        let winner = false;

        //Create buttons and append to DOM
        tagName.forEach(tag => {
            let button = document.createElement('Button');
            button.innerHTML = tag;
            button.classList.add('btn');
            button.classList.add('btn-primary');
            button.classList.add('mr-3');
            buttons.appendChild(button);
        });

        //Fetch pictures from tumblr 
        fetch(`https://api.tumblr.com/v2/tagged?tag=${randomTag}&api_key=${apiKey}`)
            .then(response => {
                return response.json();
            })
            .then(data => {
                console.log(data);
                data.response.forEach(function(post) {
                if (post.photos) {
                    post.photos.forEach(function(photo) {
                    let image = document.createElement("img");
                    let photoUrl = photo.original_size.url;

                    image.src = photoUrl;
                    image.style.width = "250px";
                    image.style.height = "250px";

                    imageContainer.appendChild(image);
                    });
                }
            });
        });

        //Check if user got correct answer or not
       
            buttons.onclick = function (event){
                if(inPlay){
                    console.log(event.target.innerHTML);
                    if (event.target.innerHTML === randomTag) {
                        let winHeading = document.createElement('h1');
                        winHeading.innerHTML = 'YOU WON';
                        winState.appendChild(winHeading);
                        inPlay = false;
                        winner = true;
            
                    } else {
                        let winHeading = document.createElement('h1');
                        winHeading.innerHTML = 'YOU LOST';
                        winState.appendChild(winHeading);
                        inPlay = false;
                    }
                } else if(!inPlay && winner) {
                    alert('You won! Click play again!')
                } else {
                    alert('You lost! Click play again!')
                }
            }
        
    }
    //Start Game
    startGame();

    //Shuffle array and return shuffled array
    function Shuffle(o) {
        for(var j, x, i = o.length; i; j = parseInt(Math.random() * i), x = o[--i], o[i] = o[j], o[j] = x);
        return o;
    };
    
    //Restart Game
    resetButton.onclick = function() {
        startGame();
    }