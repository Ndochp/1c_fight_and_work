[[Python]]
[Источник](https://stackoverflow.com/questions/2969481/ntlm-authentication-in-python)
```python
import win32com.client
url = 'https://erp.ptsecurity.com/ERP/hs/pt/TelegramInfo/aminin'
h = win32com.client.Dispatch('WinHTTP.WinHTTPRequest.5.1')
h.SetAutoLogonPolicy(0)
h.Open('GET', url, False)
h.Send()
result = h.responseText
print( result)

```