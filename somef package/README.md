# SM2KG
Software Metadata 2 Knowledge Graphs: A tool for automatically extracting relevant information from readme files

#### Installation Instructions - 

`pip3 install -r requirements.txt`

Open a python3 instance and run the following commands -

`import nltk`

`nltk.download('wordnet')`

Configuration:

Create a config.json file using the sample file in the repository and store it at `~/.somef/config.json`.

Path to the corresponding Model files are provided as shown in the sample config file.

Optional Authentication:

Add the following line to the config.json to add Authentication for requests to github repository:

`"Authorization": "token PersonalAccessToken"`

Information on generating Personal Access Token - https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line

## Command Line Interface - 

cli.py generates a JSON object after extracting useful information from the github repository. It classifies the readme file into one of four categories - description, invocation, installation, citation depending on confidence above a given threshold.

The cli.py file takes as input the following parameters:

-r / --repo_url: Link to the github repository for extracting information

-o / --output: Output file name

-t / --threshold: Threshold to classify the content of the readme file

-d / --doc_src: Path of documentation file

-g / --graph_out: (Optional) If given, the CLI will turn the SoMEF output into a Knowledge Graph and save it to the
turtle (.ttl) file given after this argument

### Add/Remove a Category:

If the user wants to run the classifier for an additional category or wants to remove an existing category, corresponding path entry in the config.json should be provided and the category type should be added/removed in the category variable in cli.py

### Github Repository Metadata:

In addition to the classified readme file, the metadata from the repository to be shown in the application is part of the keep_keys variable. If more information is to be added/removed then it should be added/removed to the keep_keys variable. 

### Example:

`python3 cli.py -r https://github.com/{owner}/{repository_name} -o output.json -t 0.5`

## Pip Package - somef:

### Temporary Installation:

- Download the requirements.txt from the repository and run 
`pip3 install -r requirements.txt`

- Open a python3 instance and run the following commands -

   `import nltk`

   `nltk.download('wordnet')`

- Run the following command

   `python3 -m pip install --index-url https://test.pypi.org/simple/ --no-deps somef`

### Instructions: 

`somef --help ` 

- will provide information on the different commands available in the package.

`somef version`

- will provide the current version of the package in the system.

`somef configure`

- user will be prompted to enter the following details:

- Authorization(optional): Users can generate a Personal Access Token from github using the link provided above.

- Description: Absolute path to the description model file. 

- Invocation: Absolute path to the description model file.

- Citation: Absolute path to the citation model file.

- Installation: Absolute path to the installation model file.

- A default model is provided with the package and will be chosen if no path is provided


`somef describe -r repository_url -t threshold -o output file`

- will run the classifier on the given repository and save it to the output file

#### Example: 

- `somef describe -r https://github.com/{owner}/{repo_name} -t 0.8 -o output.json`
