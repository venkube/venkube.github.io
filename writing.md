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

---
layout: default
title: Writing
nav_order: 4
---

## Latest Articles

<div id="medium-posts">
  Loading posts...
</div>

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
          <div style="margin-bottom:30px;">
            ${imageUrl ? `<img src="${imageUrl}" style="width:100%; max-width:600px; border-radius:8px;"><br><br>` : ""}
            <h3>
              <a href="${post.link}" target="_blank">
                ${post.title}
              </a>
            </h3>
            <p style="color: gray;">
              ${post.pubDate.substring(0,10)}
            </p>
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
