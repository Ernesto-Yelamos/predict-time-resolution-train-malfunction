#import flask
from flask import Flask, render_template, request

from W9_Project_Function import run_model_15

from gevent.pywsgi import WSGIServer

#create a flask object
app = Flask(__name__)

#create route 
#use decorators to create routes 

# for each route you define one python function to be executed (and this will be the result)
@app.route('/', methods = ['POST','GET'])
def index():
    # the python logic that will be run when the route is called
    if request.method == 'POST':
        # do stuff
        parameter_1 = request.form['parameter_1']
        parameter_2 = request.form['parameter_2']
        parameter_3 = request.form['parameter_3']
        parameter_4 = request.form['parameter_4']
        parameter_5 = request.form['parameter_5']
        parameter_6 = request.form['parameter_6']
        parameter_7 = request.form['parameter_7']
        parameter_8 = request.form['parameter_8']
        parameter_9 = request.form['parameter_9']
        
        prediction = run_model_15([parameter_1,parameter_2,parameter_3,parameter_4,parameter_5,parameter_6,parameter_7,parameter_8,parameter_9])
        print("You can expect to wait ", prediction, "for the malfunction to be resolved.")
        
        return render_template('W9_template.html', predictions = [prediction])
    else:
        return render_template('W9_template.html')
    
#running our flask app
if __name__ == "__main__" : 
    app.run(debug = False)
    app.run(host='0.0.0.0')

http_server = WSGIServer(('', 5000), app)
http_server.serve_forever()