<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Niraj's GitHub Portfolio</title>
<style>
  body { font-family: Arial, sans-serif; margin: 20px; background: #f4f4f4; }
  h1 { text-align: center; }
  .repo { background: white; padding: 15px; margin: 10px 0; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
  .repo a { color: #007acc; text-decoration: none; font-weight: bold; }
</style>
</head>
<body>
<h1>🚀 Niraj's GitHub Portfolio</h1>
<div id="repos">Loading projects...</div>

<script>
const username = "Nirajs789";
fetch(`https://api.github.com/users/${username}/repos`)
  .then(res => res.json())
  .then(data => {
    const container = document.getElementById("repos");
    container.innerHTML = "";
    data.forEach(repo => {
      container.innerHTML += `
        <div class="repo">
          <a href="${repo.html_url}" target="_blank">${repo.name}</a>
          <p>${repo.description || "No description"}</p>
        </div>
      `;
    });
  })
  .catch(err => {
    document.getElementById("repos").innerText = "Error loading repos.";
    console.error(err);
  });
</script>
</body>
</html>


