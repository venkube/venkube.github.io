---
layout: default
title: Writing
nav_order: 4
---

---

👉 [Read my articles on Medium](https://medium.com/@venkube)

I write about:

- Kubernetes architecture
- AWS best practices
- Reliability engineering patterns
- Cloud-native infrastructure

## Latest Articles

<div id="medium-posts" class="posts-grid">
  Loading posts...
</div>

<style>
.posts-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 24px;
  margin-top: 30px;
}

.post-card {
  border-radius: 12px;
  overflow: hidden;
  background: #111;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.post-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.3);
}

.post-card img {
  width: 100%;
  height: 180px;
  object-fit: cover;
}

.post-content {
  padding: 16px;
}

.post-content h3 {
  font-size: 1rem;
  margin: 0 0 8px 0;
}

.post-content p {
  font-size: 0.85rem;
  color: #aaa;
  margin: 0;
}

.post-content a {
  text-decoration: none;
  color: inherit;
}
</style>

<script>
document.addEventListener("DOMContentLoaded", function () {

  const container = document.getElementById("medium-posts");

  fetch("https://api.rss2json.com/v1/api.json?rss_url=https://medium.com/feed/@venkube")
    .then(response => response.json())
    .then(data => {

      if (!data.items) {
        container.innerHTML = "Unable to load posts.";
        return;
      }

      let html = "";

      data.items.forEach(post => {

        let imgMatch = post.content.match(/<img[^>]+src="([^">]+)"/);
        let imageUrl = post.thumbnail || (imgMatch ? imgMatch[1] : "");

        html += `
          <div class="post-card">
            <a href="${post.link}" target="_blank">
              ${imageUrl ? `<img src="${imageUrl}" alt="Thumbnail">` : ""}
              <div class="post-content">
                <h3>${post.title}</h3>
                <p>${post.pubDate.substring(0,10)}</p>
              </div>
            </a>
          </div>
        `;
      });

      container.innerHTML = html;
    })
    .catch(error => {
      container.innerHTML = "Unable to load posts.";
    });

});
</script>
