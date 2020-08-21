# ConsultaSQL
Documento de consulta para SQL.

COMANDOS:

SELECT * FROM MINHA_TABELA;

INSERT INTO MINHA_TABELA (CAMPOS) VALUES("VALORES");

UPDATE MINHA_TABELA SET CAMPO="NOVO VALOR" WHERE ID =1;

DELETE FROM MINHA_TABELA;
	
#
- Ainda há outras cláusulas:

WHERE: indica as condições

GROUP BY: realiza agrupamentos

ORDER BY: ordena os dados

#
- Ainda podemos combinar buscas com operadores lógicos.

AND: avalia se duas condições são verdadeiras

OR: avalia se uma condição é verdadeira

NOT: negação

#
- Operadores relacionais permitem fazer comparações nas consultas:

'< Menor'
 
'< Maior'
 
'<= Menor ou igual'
 
'>= Maior ou igual'
 
'= Igual'
 
'<> Diferente'
 
 'between 'entre''
 
#
- as = utilizado no campo de colunas pesquisadas para mudar o nome da coluna;

select ST.customer_name as Passageiro

#
- in = É utilizado para limitar as pesquisas de uma coluna com os valores;

where (STF.code_return in (100, 150))

#
- ::date = É utilizado para converter os valores para data;

where (ST.ts_saled::date = '2020-01-07')

#
EXEMPLO:

	select ST.customer_name as Passageiro, 
	ST.price_base as Tarifa,
	ST.price_board_tax as tx_Embarque,
	ST.price_insurance as Seguro,
	ST.price_toll as custos_extras,
	ST.price_discount as descontos,
	ST.status_id as status
		from sisb_ticket ST, sisb_ticket_fiscal STF
			where (ST.id = STF.ticket_id) 
			and (ST.ts_saled::date = '2020-01-07')
			and (STF.code_return in (100, 150))
			and (ST.ts_canceled is null)
			and (ST.status_id in (1,4,5))

#
- BETWEEN 10 AND 20 (Serve para fazer a pesquisa entre dois valores).

#
- Join serve para juntar cruzar as informações de duas tabelas.

EXEMPLO:

from "tabela 1"
JOIN "tabela 2" ON "campo tabela 1" = "campo tabela 2"


select su."name",su.username,sg.id,sg."name" from sisb_user su 
	join sisb_user_usergrp suu on suu.user_id = su.id
	join sisb_usergroup sg on sg.id = suu.usergrp_id 
	where sg.id = 12
        
#       
- SELECT COUNT(id) from "tabela";
