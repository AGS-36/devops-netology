#1

{
    "info" : "Sample JSON output from our service\t",
    "elements" : [
        {
            "name" : "first",
            "type" : "server",
            "ip" : 7175
        },
        {
            "name" : "second",
            "type" : "proxy",
            "ip" : "71.78.22.43"
        }
    ]
}

#2
import socket
import os.path
import pickle
import json
import yaml


SERVICES = ['google.com', 'drive.google.com', 'mail.google.com', 'amazon.com']


def compare_id(new_dictionary):
    with open('domain_ip.txt', 'rb') as f:
        old_dictionary = pickle.load(f)
    for key in new_dictionary.keys():
        if new_dictionary[key] == old_dictionary[key]:
            print(f'<{key}> - <{new_dictionary[key]}>')
        else:
            print(f'ERROR {key} IP mismatch: <{old_dictionary[key]}> <{new_dictionary[key]}>')
    create_dictionary(new_dictionary)


def stdout(data):
    for item in data.items():
        print(f'<{item[0]}> - {item[1]}')


def create_dictionary(data):
    with open('domain_ip.txt', 'wb') as f:
        pickle.dump(data, f)
    with open('data_file.json', 'w') as f:
        json.dump(data, f)
    with open('data_file.yaml', 'w') as f:
        yaml.dump(data, f, default_flow_style=False)

def check_dictionaty(data):
    if os.path.isfile('domain_ip.txt'):
        compare_id(data)
    else:
        create_dictionary(data)
        stdout(data)


def create_dictionary_domain_ip(domains):
    dictionary = {}
    for domain in domains:
        ip = socket.gethostbyname(domain)
        dictionary[domain] = ip
    return dictionary


if __name__ == "__main__":
    dictionary = create_dictionary_domain_ip(SERVICES)
    check_dictionaty(dictionary)

