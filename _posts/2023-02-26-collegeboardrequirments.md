---
description: Blog Time
title: College Board Requirements in my code
toc: true 
layout: default
badges: true
categories: [Final]
layout: notebook
---

### Row 1 Purpose and Function

- The purpose of our overall project is for people who want a plan to go to san diego and don't know what to do
- It serves as a planner and recorder to make the best decisions
- My program specifically works to give the user a way to see if other people enjoyed the activity they are considering
- They can also leave their own feedback

### Row 2 Data Abstraction

##### Code Segmant 1:

class Yelp(db.Model):
    __tablename__ = 'yelp'  # table name is plural, class name is singular

    # Define the User schema with "vars" from object
    id = db.Column(db.Integer, primary_key=True)
    _name = db.Column(db.String(255), unique=False, nullable=False)
    _rating = db.Column(db.String(255), unique=False, nullable=False)
    _review = db.Column(db.String(255), unique=False, nullable=False)
    _activity = db.Column(db.Integer, unique=False, nullable=False)


    # constructor of a User object, initializes the instance variables within object (self)
    def __init__(self, name, rating="five", review="super good", activity='seaworld'):
        self._name = name    # variables with self prefix become part of the object, 
        self._rating = rating
        self._review = review
        self.activity = activity

##### Code Segmant 2:

def initYelp():
    with app.app_context():
        """Create database and tables"""
        db.init_app(app)
        db.create_all()
        """Tester data for table"""
        y1 = Yelp(name='Thomas Edison', rating='five', review='good', activity='seaworld')
        y2 = Yelp(name='Nicholas Tesla', rating='five', review='good', activity='del mar')
        y3 = Yelp(name='Alexander Graham Bell', rating='five', review='good', activity='petco park')
        y4 = Yelp(name='Eli Whitney',  rating='five', review='good', activity='seaworld')
        y5 = Yelp(name='John Mortensen', rating='five', review='good', activity='del mar')

- My response shows two distinct code segmants that are showing data being stored and the accessing of the code and how it is managed

### Row 3 Managing Complexity

def create(self):
        try:
            # creates a person object from User(db.Model) class, passes initializers
            db.session.add(self)  # add prepares to persist person object to Users table
            db.session.commit()  # SqlAlchemy "unit of work pattern" requires a manual commit
            return self
        except IntegrityError:
            db.session.remove()
            return None

    # CRUD read converts self to dictionary
    # returns dictionary
    def read(self):
        return {
            "id": self.id,
            "name": self.name,
            "rating": self.rating,
            "review": self.review,
            "activity": self.activity,

- These two sections to my code show how the data in the database is being stored and accesed in order to manage complexity.
- These make it easier to store the data in a table depending on the section
- It shows the name, activity, rating, etc, all separated.

### Row 4 Procedural Abstraction

class _Read(Resource):
        def get(self):
            yelp = Yelp.query.all()    # read/extract all users from database
            json_ready = [yelp.read() for yelp in yelp]  # prepare output in json
            return jsonify(json_ready)  # jsonify creates Flask response object, more specific to APIs than json.dumps
    
    class _Security(Resource):

        def post(self):
            ''' Read data for json body '''
            body = request.get_json()

- This shows the different functions of updating and the parameters.
- It shows the conditions and it will return the json if the conditions are met and the parameters

### Row 5 Algorithm implentation

def update(self, name="", rating="", review="", activity=""):
        """only updates values with length"""
        if len(name) > 0:
            self.name = name
        if len(rating) > 0:
            self.rating = rating
        if len(review) > 0:
            self._review = review
        if len(activity) > 0:
            self.activity = activity
        db.session.commit()
        return self

- This code segmant shows the if statements and how the different sections of the table are sequenced and how it will be returned

### Row 6 Testing

- The results of the program will show the data I stored separated by the category
- There is the names, ratings, reviews, etc.
- I will also have a section where these categories can be entered and added to the table with CRUD