
local http = require("socket.http")
local json = require("dkjson")  -- Biblioteca JSON para manipulaÃ§Ã£o de dados


    local url = "https://api.cartolafc.globo.com/atletas/mercado"
    local resposta, status = http.request(url)

    if status == 200 then
        local dados = json.decode(resposta)
        return dados.athletes
    else
        print("Erro ao obter dados: " .. status)
        return nil
    end
end


function obterTime(time_id)
    local url = "https://api.cartolafc.globo.com/time/" .. time_id
    local resposta, status = http.request(url)

    if status == 200 then
        local dados = json.decode(resposta)
        return dados
    else
        print("Erro ao obter dados: " .. status)
        return nil
    end
end


local jogadores = obterJogadores()
if jogadores then
    print("Jogadores disponÃ­veis:")
    for i, jogador in ipairs(jogadores) do
        print(jogador.nome)
    end
end


local time_id = 123456  -- Substitua com o ID do seu time
local time = obterTime(time_id)
if time then
    print("InformaÃ§Ãµes do time:")
    print("Nome do time: " .. time.nome)
    print("PontuaÃ§Ã£o: " .. time.pontos)
end
