<script>
(function(){
    var feedUrl = "https://globalsell.site/feeds/posts/default?alt=json";
    var indexNowKey = "YOUR_KEY_FOR_GLOBALSELL_SITE"; // এখানে আপনার API key দিন

    fetch(feedUrl)
    .then(r => r.json())
    .then(data => {
        var postUrl = data.feed.entry[0].link.find(l => l.rel === "alternate").href;

        // Google Ping
        fetch("https://www.google.com/ping?sitemap=" + encodeURIComponent(postUrl));

        // Bing IndexNow
        fetch("https://api.indexnow.org/indexnow?url=" + encodeURIComponent(postUrl) + "&key=" + indexNowKey);

        // Yandex Ping
        fetch("https://yandex.com/ping?sitemap=" + encodeURIComponent(postUrl));

        console.log("Index requests sent for: " + postUrl);
    })
    .catch(err => console.error("Error fetching feed:", err));
})();
</script>
