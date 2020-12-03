import pickle

def run_model_15(mylist):
    my_dict = {'a':'0-15 minutes', 'b':'15-30 minutes', 'c':'30-45 minutes', 'd':'45-60 minutes', 'e':'60-75 minutes', 'f':'75-90 minutes', 'g':'90-105 minutes', 'h':'105-120 minutes', 'i':'120-135 minutes', 'j':'135-150 minutes','k':'150-165 minutes', 'l':'165-180 minutes', 'm':'180-195 minutes', 'n':'195-210 minutes', 'o':'210-225 minutes', 'p':'225-240 minutes', 'q':'240-255 minutes', 'r':'255-270 minutes', 's':'270-285 minutes','t':'285-300 minutes'}
    new_data = mylist
    with open('encoder.pkl', 'rb') as f:
        enc = pickle.load(f)
    encoded = enc.transform([new_data]) 
    pkl_filename = "W9-project-model-class-15-ohe.pkl"
    # Load from file
    with open(pkl_filename, 'rb') as file:
        pickle_model = pickle.load(file)
    prediction = pickle_model.predict(encoded)
    pred = list(str(prediction))[2]
    return (my_dict[pred])