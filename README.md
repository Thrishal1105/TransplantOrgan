// dockerfile
FROM python:3.8

WORKDIR /app

COPY . .

RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 5000

CMD ["python", "app.py"]

// requirements txt
Flask==1.1.2

// app.py
from flask import Flask, request, render_template

app = Flask(__name__)

@app.route('/register', methods=['GET', 'POST'])
def register():
    if request.method == 'POST':
        name = request.form['name']
        email = request.form['email']
        password = request.form['password']
        # Store the user data in a database or file (this step is a placeholder)
        return render_template('success.html')
    return render_template('register.html')

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
    
// template in register.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Registration</title>
</head>
<body>
    <h1>Register for the Event</h1>
    <form method="post">
        <input type="text" name="name" placeholder="Name" required><br><br>
        <input type="email" name="email" placeholder="Email" required><br><br>
        <input type="password" name="password" placeholder="Password" required><br><br>
        <button type="submit">Register</button>
    </form>
</body>
</html>

// success.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registration Successful</title>
</head>
<body>
    <h1>Registration Successful!</h1>
    <p>Thank you for registering for the event.</p>
</body>
</html>


//build
docker build -t user-registration .

//run
docker run -p 5000:5000 user-registration

