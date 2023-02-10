# WSS_CRUD05.js
#Demonstre como fazer as quatro operações de CRUD e suas rotas para obter o recurso de um livro que está no estoque de uma livraria. Um livro possui informações como nome, autor e ISBN.

Aqui está um exemplo de como implementar as operações de CRUD para um livro em JavaScript usando o framework Express:

const express = require('express');
const app = express();
const port = 3000;

// In-memory data store for books
let books = [
  { id: 1, name: 'Livro 1', author: 'Autor 1', ISBN: '123-456-789' },
  { id: 2, name: 'Livro 2', author: 'Autor 2', ISBN: '987-654-321' }
];

// Create a new book
app.post('/api/livros', (req, res) => {
  const book = {
    id: books.length + 1,
    name: req.body.name,
    author: req.body.author,
    ISBN: req.body.ISBN
  };
  books.push(book);
  res.status(201).send(book);
});

// Read a single book by ID
app.get('/api/livros/:id', (req, res) => {
  const book = books.find(b => b.id === parseInt(req.params.id));
  if (!book) {
    return res.status(404).send('The book with the given ID was not found.');
  }
  res.send(book);
});

// Update a book by ID
app.put('/api/livros/:id', (req, res) => {
  const book = books.find(b => b.id === parseInt(req.params.id));
  if (!book) {
    return res.status(404).send('The book with the given ID was not found.');
  }
  book.name = req.body.name;
  book.author = req.body.author;
  book.ISBN = req.body.ISBN;
  res.send(book);
});

// Delete a book by ID
app.delete('/api/livros/:id', (req, res) => {
  const book = books.find(b => b.id === parseInt(req.params.id));
  if (!book) {
    return res.status(404).send('The book with the given ID was not found.');
  }
  const index = books.indexOf(book);
  books.splice(index, 1);
  res.send(book);
});

app.listen(port, () => {
  console.log(`Listening at http://localhost:${port}`);
});
