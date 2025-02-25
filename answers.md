// Connect to MongoDB and create the database
use library;

// Create and insert books into the collection
db.books.insertMany([
{ title: "The Great Gatsby", author: "F. Scott Fitzgerald", publishedYear: 1925, genre: "Fiction", ISBN: "9780743273565" },
{ title: "1984", author: "George Orwell", publishedYear: 1949, genre: "Dystopian", ISBN: "9780451524935" },
{ title: "The Catcher in the Rye", author: "J.D. Salinger", publishedYear: 1951, genre: "Fiction", ISBN: "9780316769488" },
{ title: "The Road", author: "Cormac McCarthy", publishedYear: 2006, genre: "Post-apocalyptic", ISBN: "9780307387899" },
{ title: "Harry Potter and the Sorcerer's Stone", author: "J.K. Rowling", publishedYear: 1997, genre: "Fantasy", ISBN: "9780590353427" }
]);

// Retrieve all books
db.books.find();

// Query books based on a specific author
db.books.find({ author: "George Orwell" });

// Find books published after the year 2000
db.books.find({ publishedYear: { $gt: 2000 } });

// Update the publishedYear of a specific book
db.books.updateOne({ ISBN: "9780451524935" }, { $set: { publishedYear: 1950 } });

// Add a new field 'rating' to all books and set a default value
db.books.updateMany({}, { $set: { rating: 5 } });

// Delete a book by its ISBN
db.books.deleteOne({ ISBN: "9780316769488" });

// Remove all books of a particular genre
db.books.deleteMany({ genre: "Dystopian" });

// Data model for an e-commerce platform
db.createCollection("users");
db.createCollection("orders");
db.createCollection("products");

// Example data for e-commerce platform
db.users.insertOne({ name: "Alice", email: "alice@example.com", address: "123 Main St" });
db.products.insertOne({ name: "Laptop", price: 1000, category: "Electronics" });
db.orders.insertOne({ userId: ObjectId("someUserId"), productId: ObjectId("someProductId"), quantity: 1, status: "Shipped" });

// Aggregation to find the total number of books per genre
db.books.aggregate([
{ $group: { _id: "$genre", totalBooks: { $sum: 1 } } }
]);

// Calculate the average published year of all books
db.books.aggregate([
{ $group: { _id: null, avgPublishedYear: { $avg: "$publishedYear" } } }
]);

// Identify the top-rated book
db.books.find().sort({ rating: -1 }).limit(1);

// Create an index on the author field
db.books.createIndex({ author: 1 });
