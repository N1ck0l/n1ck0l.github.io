---
layout: default
title: Buscar Posts
permalink: /buscar/
---

<div class="search-page">
  <h1 class="search-title">🔍 Buscar Posts</h1>
  
  <div class="search-container">
    <input 
      type="text" 
      id="searchInput" 
      class="search-input" 
      placeholder="Digite sua busca aqui..."
      autocomplete="off"
    >
    <span id="searchCount" class="search-count"></span>
  </div>

  <div id="searchResults" class="search-results">
    <!-- Resultados aparecem aqui -->
  </div>

  <div id="noResults" class="no-results" style="display: none;">
    <p>😔 Nenhum post encontrado para "<strong id="searchTerm"></strong>"</p>
    <p>Tente usar outras palavras-chave ou <a href="/arquivo/">explore o arquivo</a></p>
  </div>
</div>

<script>
// Função de busca
let allPosts = [];

// Carregar posts
fetch('{{ "/search.json" | relative_url }}')
  .then(response => response.json())
  .then(data => {
    allPosts = data;
    handleSearch(); // Buscar se houver query na URL
  });

// Event listener para input de busca
const searchInput = document.getElementById('searchInput');
searchInput.addEventListener('keyup', handleSearch);
searchInput.addEventListener('input', handleSearch);

function handleSearch() {
  const query = searchInput.value.toLowerCase().trim();
  const resultsContainer = document.getElementById('searchResults');
  const noResultsDiv = document.getElementById('noResults');
  const searchCountDiv = document.getElementById('searchCount');
  
  if (query.length === 0) {
    resultsContainer.innerHTML = '';
    noResultsDiv.style.display = 'none';
    searchCountDiv.textContent = '';
    return;
  }

  // Filtrar posts
  const filtered = allPosts.filter(post => {
    const searchText = `${post.title} ${post.content} ${post.categories} ${post.excerpt}`.toLowerCase();
    return searchText.includes(query);
  });

  // Exibir resultados
  if (filtered.length === 0) {
    resultsContainer.innerHTML = '';
    noResultsDiv.style.display = 'block';
    document.getElementById('searchTerm').textContent = query;
    searchCountDiv.textContent = '';
  } else {
    noResultsDiv.style.display = 'none';
    resultsContainer.innerHTML = filtered.map(post => `
      <div class="search-result-item">
        <h3><a href="${post.url}" class="search-result-link">${post.title}</a></h3>
        <div class="search-result-meta">
          <span class="search-result-date">📅 ${post.date}</span>
          <span class="search-result-category">${post.categories}</span>
        </div>
        <p class="search-result-excerpt">${post.excerpt}</p>
      </div>
    `).join('');
    
    searchCountDiv.textContent = `${filtered.length} resultado${filtered.length !== 1 ? 's' : ''}`;
  }
}

// Suportarpré-busca via URL
document.addEventListener('DOMContentLoaded', function() {
  const params = new URLSearchParams(window.location.search);
  const query = params.get('q');
  if (query) {
    searchInput.value = decodeURIComponent(query);
    handleSearch();
  }
});
</script>
