# PLC Manager

Aplicação web Flask + MySQL + Bootstrap + DataTables para gerenciamento de PLCs.

## Estrutura

- `app.py`: rotas e aplicação Flask
- `database.py`: conexão e execução de consultas MySQL
- `config.py`: configuração do banco
- `templates/`: páginas HTML
- `static/css/`: estilos
- `static/js/`: DataTables

## Instalação

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

Linux/macOS:

```bash
source .venv/bin/activate
```

Depois:

```bash
pip install -r requirements.txt
```

Edite `config.py` com as credenciais do MySQL.

Execute:

```bash
python app.py
```

Acesse:

`http://localhost:5000`

## Observação

O dashboard utiliza a consulta:

```sql
SELECT
    p.id AS PLC_ID,
    p.name AS PLC_Nome,
    p.enumerator_factory AS Factory,
    p.ip_address AS IP,
    p.port AS Porta,
    e.name AS Equipamento,
    et.name AS Tipo,
    e.memory_address AS Endereco_Memoria
FROM plc_controllers p
JOIN equipments e ON e.plc_id = p.id
JOIN equipment_types et ON e.equipment_type_id = et.id
ORDER BY p.id;
```

O cadastro utiliza:

```sql
INSERT INTO plc_controllers
    (name, enumerator_factory, ip_address, port)
VALUES (%s, %s, %s, %s);
```
