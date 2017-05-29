import re
import json
import traceback
import boto3

s3_resource = boto3.resource('s3')
s3_client = boto3.client('s3')
dynamodb_client = boto3.client('dynamodb')

table_name = 'lambda_dynamodb_table'

def lambda_handler(event, context):
    bucket_name = event['Records'][0]['s3']['bucket']['name']
    key = event['Records'][0]['s3']['object']['key']
    if not key.endswith('/'):
        try:
            split_key = key.split('/')
            file_name = split_key[-1]
            item = {'key': {'S': file_name}}
            dynamodb_client.delete_item(TableName=table_name, Key=item)
        except Exception as e:
            print(traceback.format_exc())

    return (bucket_name, key)
