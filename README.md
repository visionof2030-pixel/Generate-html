<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>فتح البث في VLC</title>

<script>
function openVLC() {
    const streamUrl = "https://amir11.bounceme.net:8080/YZjwcwnLjh/QlXrgJTnED/1127";
    const ua = navigator.userAgent || navigator.vendor || window.opera;

    if (/android/i.test(ua)) {
        window.location.href =
            "intent://" +
            streamUrl.replace(/^https?:\/\//, "") +
            "#Intent;scheme=https;package=org.videolan.vlc;end";
    } else {
        window.location.href = "vlc://" + streamUrl;
    }
}

window.onload = function() {
    openVLC();
};
</script>

<style>
body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin-top: 100px;
}
button {
    padding: 12px 24px;
    font-size: 18px;
}
</style>
</head>
<body>

<h2>جاري فتح البث في VLC...</h2>

<p>إذا لم يفتح VLC تلقائياً اضغط الزر:</p>

<button onclick="openVLC()">
فتح في VLC
</button>

</body>
</html>