
* Example: Using async/await (see [[JS - Async & Await]])
```js
const imgContainer = document.querySelector('.images');

const createImage = function (imgPath) {
	return new Promise(function (resolve, reject) {
		const img = document.createElement('img');
	    img.src = imgPath;
	    img.addEventListener('load', () => {
			imgContainer.append(img);
		    resolve(img);
	    });
	    img.addEventListener('error', () => {
		    reject(new Error('Image not found'));
	    });
	});
};


// Using an aysnc/await function
const loadNPause = async () => {
	try {
		let img = await createImage('img/img-1.jpg');
		console.log('Image 1 loaded');
	    await wait(2);
	    img.style.display = 'none';
	    
	    img = await createImage('img/img-2.jpg');
	    console.log('Image 2 loaded');
	    await wait(2);
	    img.style.display = 'none';
	    
	} catch (err) {
		console.error(err);
	}
};

loadNPause();
```

* Example: async/await with the Promise.all() [[JS - Promise Methods]]
```js
// Using an aysnc/await function
const loadAll = async (imgArr) => {
	try {
		let imgs = imgArr.map(async img => await
	    createImage(img));
	    const imgsEl = await Promise.all(imgs);
	    console.log(imgEls);
	    imgELs.forEach((img) => {
		    img.classList.add('parrallel');
	    })
	} catch (err) {
		console.error(err);
	}
};

loadAll(['img/img-1.jpg', 'img/img-2.jpg', 'img/img-3.jpg']);
```