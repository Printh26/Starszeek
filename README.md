// Fonction pour afficher ou masquer le menu hamburger
function toggleMenu() {
  const menu = document.getElementById('menu');
  menu.style.display = menu.style.display === 'block' ? 'none' : 'block';
}

// Fonction de recherche dans le menu
function searchMusic() {
  const searchTerm = document.getElementById('searchBar').value.toLowerCase();
  const searchResults = document.getElementById('searchResults');
  searchResults.innerHTML = ''; // Vider les résultats

  const filteredSongs = songs
    .map((song, index) => ({ ...song, index })) // Associer chaque chanson avec son index
    .filter(song => song.title.toLowerCase().includes(searchTerm));

  if (filteredSongs.length > 0) {
    filteredSongs.forEach(song => {
      const songElement = document.createElement('div');
      songElement.textContent = song.title;
      songElement.dataset.index = song.index; // Stocker l'index réel
      songElement.addEventListener('click', () => loadSong(parseInt(songElement.dataset.index)));
      searchResults.appendChild(songElement);
    });
  } else {
    searchResults.innerHTML = 'Aucune musique trouvée';
  }
}
