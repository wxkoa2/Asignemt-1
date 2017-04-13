# Assignment-1
//Angelene
//WeiXin
var listOfAllKnownAuthors = []

class BookStore
{
    constructor(name, address, owner)
    {
        this._name = name;
        this._address = address;
        this._owner = owner;
        this._booksAvailable = [];
        this._totalCopiesOfAllBooks = 0
    }

    authorKnown(authorName)
    {
        var foundThem = false;
        for (var pos = 0; pos < listOfAllKnownAuthors.length; pos++)
        {
            if (authorName === listOfAllKnownAuthors[pos])
            {
                foundThem = true
            }
        }
        return foundThem
    }

    addBook(bookInstance, copies)
    {
        var positionOfBook = this.checkForBook(bookInstance);
        if (positionOfBook != null)
        {
             this._booksAvailable[positionOfBook].copies += copies;
             console.log("Added " + copies + " copies of " + bookInstance);
             listOfAllKnownAuthors.push(bookInstance.author);
        }
        else
        {
             var bookCopies = {
                 book: bookInstance,
                 copies: copies
             };
             this._booksAvailable.push(bookCopies);
             console.log("Added " + copies + " copies of a new book: " + bookInstance);
        }

        this._totalCopiesOfAllBooks += copies;
    }

    sellBook(bookInstance, numberSold)
    {
        var positionOfBook = this.checkForBook(bookInstance);
        if (positionOfBook != null)
        {
            if (numberSold > this._booksAvailable[positionOfBook].copies)
            {
                console.log("Not enough copies of " + BookInstance + " to sell");
            }
            else
            {
                this._booksAvailable[positionOfBook].copies -= numberSold;
                if (this._booksAvailable[positionOfBook].copies === 0)
                {
                    this._booksAvailable.pop(PositionOfBook);
                    this._NumTitles -= 1;
                    var foundAuth = this.authorKnown(bookInstance.author);
                    listOfAllKnownAuthors.pop(foundAuth);
                }
                this._totalCopiesOfAllBooks -= numberSold;
                console.log("Sold " + numberSold + " copies of " + bookInstance);
            }
        }
        else
        {
            console.log(bookInstance + " not found");
        }
    }

    checkForBook(bookInstance)
    {
        var currBookNum = 0;
        while (currBookNum < this._booksAvailable.length)
        {
            if (this._booksAvailable[currBookNum].book === bookInstance)
            {
                return currBookNum;
            }
            else
            {
                return null;
            }
            currBookNum += 1;
        }
        return null;
    }

    get name()
    {
        return this._name;
    }

    set name(newName)
    {
        this._name = newName;
    }

    get address()
    {
        return this._address;
    }

    set address(newAddress)
    {
        this._address = newAddress;
    }

    get owner()
    {
        return this._owner;
    }

    set address(newOwner)
    {
        this._owner = newOwner;
    }
}

class Book
{
    constructor(title, author, publicationYear, price)
    {
        this._title = title;
        this._author = author;
        this._publicationYear = publicationYear;
        this._price = price;
        if (this.authorKnown(this._author) === false)
        {
            listOfAllKnownAuthors.push(this._author)
        }
    }

    authorKnown(authorName)
    {
        var foundThem = false;
        for (var pos = 0; pos < listOfAllKnownAuthors.length; pos++)
        {
            if (authorName === listOfAllKnownAuthors[pos])
            {
                foundThem = true;
            }
        }
        return foundThem;
    }

    get title()
    {
        return this._title;
    }

    get author()
    {
        return this._author;
    }

    get publicationYear()
    {
        return this._publicationYear;
    }

    get price()
    {
        return this._price;
    }

    toString()
    {
        return this.title + ", " + this.author + ". " + this.publicationYear + " ($" + this.price + ")";
    }
}

// Book details courtesy of Harry Potter series by J.K. Rowling

var flourishAndBlotts = new BookStore("Flourish & Blotts", "North side, Diagon Alley, London, England", "unknown");
var monsterBook = new Book("The Monster Book of Monsters", "Edwardus Lima", 1978, 40);
var monsterBookToSell = new Book("The Monster Book of Monsters", "Edwardus Lima", 1978, 40);
flourishAndBlotts.addBook(monsterBook, 500);
flourishAndBlotts.sellBook(monsterBookToSell, 200);
var spellBook = new Book("The Standard Book of Spells, Grade 4", "Miranda Goshawk", 1921, 80);
flourishAndBlotts.addBook(spellBook, 40);
flourishAndBlotts.addBook(spellBook, 20);
flourishAndBlotts.sellBook(spellBook, 15);
flourishAndBlotts.addBook(monsterBookToSell, 30);
flourishAndBlotts.sellBook(monsterBookToSell, 750);

console.log("Authors known: " + listOfAllKnownAuthors);
