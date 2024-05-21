# image-search

![image](https://github.com/jung-chaewon/image-search/assets/131144717/2cda5311-b92b-48a4-ab42-7c7331cd964a)

자바스크립트를 이용한 이미지검색 사이트 만들기
### script
  // API 키
const accessKey = "RZEIOVfPhS7vMLkFdd2TSKGFBS4o9_FmcV1Nje3FSjw"; // 실제 API 키는 사용하지 마세요!

// 선택자
const formEl = document.querySelector("form");
const searchInputEl = document.getElementById("search-input");
const searchResultsEl = document.querySelector(".search-results");
const showMoreButtonEl = document.getElementById("show-more-button");


let inputData = "";
let page = 1;


async function searchImages() {

  inputData = searchInputEl.value;


  const url = `https://api.unsplash.com/search/photos?page=${page}&query=${inputData}&client_id=${accessKey}`;


  const response = await fetch(url);
  const data = await response.json();

  
  if (page === 1) {
    searchResultsEl.innerHTML = "";
  }


  const results = data.results;


  results.map((result) => {

    const imageWrapper = document.createElement("div");
    imageWrapper.classList.add("search-result");

    const image = document.createElement("img");
    image.src = result.urls.small;
    image.alt = result.alt_description;

    const imageLink = document.createElement("a");
    imageLink.href = result.links.html;
    imageLink.target = "_blank";
    imageLink.textContent = result.alt_description;

    imageWrapper.appendChild(image);
    imageWrapper.appendChild(imageLink);

    searchResultsEl.appendChild(imageWrapper);
  });

  page++;

  if (page > 1) {
    showMoreButtonEl.style.display = "block";
  }
}

formEl.addEventListener("submit", (event) => {
  event.preventDefault();
  page = 1;
  searchImages();
});

showMoreButtonEl.addEventListener("click", () => {
  searchImages();
});

###
