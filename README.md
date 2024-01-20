<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitHub Repositories</title>
    <style>
        body{
            font-family: arial, sans-serif;
            margin : 10px;
            padding : 10px;
        }

        repository-container{
            display : flex;
            flex-wrap : wrap;
            justify-content : space-between;
        }
        
        repository{
            width : 30%;
            border : 5px solid #064874;
            padding : 15px;
            margin : 10px;
            box-sizing : border-box;
        }
    </style>
</head>
<body>
    <h1>GitHub Repositories</h1>
    <label for="username">GitHub Username:</label>
    <input type="text" id="username" placeholder="Enter GitHub Username">
    <button onclick="fetchRepos()">Fetch Repos</button>

    <div id="repos"></div>

    <div id="pagination">
        <button onclick="previousPage()">Previous</button>
        <span>Page <span id="currentPage">1</span> of <span id="totalPages">1</span></span>
        <button onclick="nextPage()">Next</button>
        <label for="reposPerPage">Repos per page:</label>
        <select id="reposPerPage" onchange="changePerPage()">
            <option value="10" selected>10</option>
            <option value="30">30</option>
            <option value="50">50</option>
            <option value="100">100</option>
        </select>
    </div>

    <script>
        let username = "";
        let currentPage = 1;
        let reposPerPage = 10;
        let totalRepos = 0;
        let totalPages = 1;

        function fetchRepos() {
            username = document.getElementById("username").value;
            currentPage = 1;

            // Fetch GitHub repositories using the GitHub API
            fetch(https://github.com/gbgabiola/johndoe-portfolio);
                .then(response => response.json())
                .then(data => {
                    totalRepos = data.length;
                    totalPages = Math.ceil(totalRepos / reposPerPage);
                    displayRepos(data);
                })
                .catch(error => console.error(error));
        }

        function displayRepos(repos) {
            const reposDiv = document.getElementById("repos");
            reposDiv.innerHTML = "";

            repos.forEach(repo => {
                const repoDiv = document.createElement("div");
                repoDiv.textContent = repo.name;
                reposDiv.appendChild(repoDiv);
            });

            document.getElementById("currentPage").textContent = currentPage;
            document.getElementById("totalPages").textContent = totalPages;
        }

        function previousPage() {
            if (currentPage > 1) {
                currentPage--;
                fetchRepos();
            }
        }

        function nextPage() {
            if (currentPage < totalPages) {
                currentPage++;
                fetchRepos();
            }
        }

        function changePerPage() {
            reposPerPage = parseInt(document.getElementById("reposPerPage").value);
            fetchRepos();
        }
    </script>
</body>
</html>
