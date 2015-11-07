# repository_personal

��� ��� ������ ����� �������, ���������� ���� (����, �������, "��������� �������") ��� ��������� ���� ��������. ��� ������� ����� repper_install � ����������� ����� ������ ��������� ������ repper. ��� ����� ������������� ����� ������� ��������� ������� �� ����������� - �� ��������� � sys.path ���������� repository_personal. ��� ��������� ������� ������ ����������� � ����� ����������, �������� ��� ��������� ���� ����� ��������.

�� ����� �� ��������������, ����� ������ ������ ������� ����������� ��� � �������� ���������� ������, ��� � ���������� � ����� ��������.

# ���������� �����������

## apitools

������ ��� �������� �������, ����������� API ��� ��������� ��������, ������� �������������� ���������. ������ �������� ����� proto_api. ���� ����� ����������� ����� ������� API, � ��� ����� ������ ��������� ������� shell, ������� ����� ������������ ��� ������ � ��������� � ���� �������. ��� ��������� �� ������ ��������� ������� ������� ��� �������. ��������, ��� ����� ����� ���� �����:
```
import repper, apitools
import urllib, urllib2, json, hashlib, os, time

class API(apitools.proto_api):
  __url = "https://api.example.com/v1/"
  def __init__(self, api_key, api_secret):
    self.__api_key = api_key
    self.__api_secret = api_secret

  def public_api(self, api_name, api_params={}):
    x = 1
    while x:
      req = urllib2.Request(self.__url + api_name+'?'+urllib.urlencode(api_params), headers={'Accept-Charset': 'utf-8' })
      x = 0
    return urllib2.urlopen(req).read()

  def shell(self, api_name, api_params):
    if api_name[0] == '_': answer = self.auth_api(api_name[1:], api_params)
    else: answer = self.public_api(api_name, api_params)

    jd = json.JSONDecoder()
    return jd.decode(answer) 
```
����� ���� �� ������ ����� ���������� � ������ ������� ������� api.example.com ��� ��������� ����������� �������:
```
api = API(key, secret)
print api.get_user_info(user_id=123456789)
```
� ���������� ����� ������ URL "https://api.example.com/v1/get_user_info?user_id=123456789" . � ������� shell ����� ����� ����������� ��������������� ��������� ������ ������� - ��������, ������.