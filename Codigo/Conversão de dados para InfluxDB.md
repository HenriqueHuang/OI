var umidade = ""
var temperatura = ""

if (typeof msg.payload === 'string' && msg.payload.toString().endsWith('%')) {
umidade = msg.payload
} else {
temperatura = msg.payload
}

msg.payload=
{
"temperatura": temperatura,
"umiadade": umidade
}
return msg;
