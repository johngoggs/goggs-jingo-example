This is a page to describe Jingo and how it is setup for this installation.

## Hosting
This content is being hosted locally to test Jingo and how it interacts with a Git repo.

### Code example
This code example is extracted from [gogs-gcp-endpointsrun](https://github.com/johngoggs/goggs-gcp-endpointsrun).

```python
from flask import Flask, jsonify

app = Flask(__name__)


@app.route('/api/status', methods=['GET'])
def get_status():
    return jsonify(message='Server is up!'), 200


@app.route('/api/auth/apikey', methods=['GET'])
def get_auth_apikey():
    return jsonify(message='Congratulations. You have completed apikey auth.',
                   auth='apikey'), 200


@app.route('/api/auth/bearer', methods=['GET'])
def get_auth_sabearer():
    return jsonify(message='Congratulations. You have completed service account bearer auth.',
                   auth='service account bearer'), 200


@app.errorhandler(400)
def bad_request_error(e):
    return jsonify(code=400,
                   message='Bad request',
                   detailedMessage='{}'.format(e)), 400


@app.errorhandler(404)
def not_found_error(e):
    return jsonify(code=404,
                   message='Path not found',
                   detailedMessage='{}'.format(e)), 404


@app.errorhandler(405)
def method_not_allowed_error(e):
    return jsonify(code=405,
                   message='Method not allowed',
                   detailedMessage='{}'.format(e)), 405


@app.errorhandler(Exception)
def internal_server_error(e):
    return jsonify(code=500,
                   message='Internal server error',
                   detailedMessage='{}'.format(e)), 500


if __name__ == '__main__':
    app.run(host='127.0.0.1', port='8080')
```