<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Loja de Livros - Arthur Martin</title>
<style>
  body { font-family: Arial, sans-serif; margin: 0; padding: 10px; background: #f0f0f0; }
  h1, h2 { color: #2d6cdf; }
  form, .book { background: white; padding: 10px; margin-bottom: 15px; border-radius: 5px; }
  input, textarea, button { width: 100%; margin: 5px 0; padding: 8px; }
  button { background: #2d6cdf; color: white; border: none; border-radius: 4px; }
  .book img { max-width: 100%; height: 150px; object-fit: cover; border-radius: 4px; }
  .book-title { font-weight: bold; font-size: 1.2em; margin: 5px 0; color: #2d6cdf; }
  .book-price { color: green; font-weight: bold; margin-bottom: 5px; }
</style>
</head>
<body>

<h1>Minha Loja de Livros</h1>

<form id="bookForm">
  <input type="hidden" id="bookId" />
  <input type="text" id="title" placeholder="Título do livro" required />
  <textarea id="description" placeholder="Descrição do livro" rows="3" required></textarea>
  <input type="number" id="price" placeholder="Preço (R$)" step="0.01" min="0" required />
  <input type="url" id="image" placeholder="URL da imagem da capa" required />
  <button type="submit">Salvar Livro</button>
</form>

<div id="booksContainer"></div>

<script>
  let books = JSON.parse(localStorage.getItem('books') || '[]');

  const form = document.getElementById('bookForm');
  const booksContainer = document.getElementById('booksContainer');

  function saveBooks() {
    localStorage.setItem('books', JSON.stringify(books));
  }

  function renderBooks() {
    booksContainer.innerHTML = '';
    if (books.length === 0) {
      booksContainer.innerHTML = '<p>Nenhum livro criado.</p>';
      return;
    }
    books.forEach(book => {
      const div = document.createElement('div');
      div.className = 'book';
      div.innerHTML = `
        <img src="${book.image}" alt="${book.title}" />
        <div class="book-title">${book.title}</div>
        <div>${book.description}</div>
        <div class="book-price">R$ ${parseFloat(book.price).toFixed(2)}</div>
        <button onclick="editBook('${book.id}')">Editar</button>
        <button onclick="deleteBook('${book.id}')">Excluir</button>
      `;
      booksContainer.appendChild(div);
    });
  }

  function generateId() {
    return '_' + Math.random().toString(36).substr(2, 9);
  }

  form.addEventListener('submit', e => {
    e.preventDefault();
    const id = document.getElementById('bookId').value;
    const title = document.getElementById('title').value.trim();
    const description = document.getElementById('description').value.trim();
    const price = document.getElementById('price').value;
    const image = document.getElementById('image').value.trim();

    if (!title || !description || !price || !image) {
      alert('Por favor, preencha todos os campos.');
      return;
    }

    if (id) {
      // Editar livro existente
      const index = books.findIndex(b => b.id === id);
      if (index !== -1) {
        books[index] = { id, title, description, price, image };
      }
    } else {
      // Adicionar novo livro
      books.push({ id: generateId(), title, description, price, image });
    }

    saveBooks();
    renderBooks();
    form.reset();
    document.getElementById('bookId').value = '';
  });

  window.editBook = function(id) {
    const book = books.find(b => b.id === id);
    if (!book) return;
    document.getElementById('bookId').value = book.id;
    document.getElementById('title').value = book.title;
    document.getElementById('description').value = book.description;
    document.getElementById('price').value = book.price;
    document.getElementById('image').value = book.image;
  }

  window.deleteBook = function(id) {
    if (!confirm('Tem certeza que deseja excluir este livro?')) return;
    books = books.filter(b => b.id !== id);
    saveBooks();
    renderBooks();
  }

  renderBooks();
</script>

</body>
</html>
