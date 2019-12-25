Задача №1
    def read():
        # Получим данные всех колонок на доске:  
        column_data = requests.get(base_url.format('boards') + '/' + board_id + '/lists', params=auth_params).json()  

        # Теперь выведем название каждой колонки и всех заданий, которые к ней относятся:  
        for column in column_data:
            # Получим данные всех задач в колонке. Мы и раньше делали это, но до этого мы только перебирали элементы этих данных, 
            # А теперь мы ещё получим общее количество задач при помощи встроенной функции `len()`:
            task_data = requests.get(base_url.format('lists') + '/' + column['id'] + '/cards', params=auth_params).json()  
            print(column['name'] + " - ({})".format(len(task_data)))  

            if not task_data:  
                print('\t' + 'Нет задач!')  
                continue  
            for task in task_data:  
                print('\t' + task['name'])
                
Задача №2

  board_id = "5d8210d0fe6fe82b22ee533e"
  response = requests.get(base_url.format('boards/' + board_id), params=auth_params).json()
  
  # функция создания колонок:  
  
   def create(name, column_name):  
    column_id = column_check(column_name)  
    if column_id is None:  
        column_id = create_column(column_name)['id']  
  
    requests.post(base_url.format('cards'), data={'name': name, 'idList': column_id, **auth_params})
  
  # возвращает ID колонки, если колонка с таким именем существует:  
  
  def column_check(column_name):  
      column_id = None  
      column_data = requests.get(base_url.format('boards') + '/' + board_id + '/lists', params=auth_params).json()  
      for column in column_data:  
          if column['name'] == column_name:  
              column_id = column['id']  
              return column_id
    
    # функция move:  
    
    def move(name, column_name):  
    # Получим данные всех колонок на доске  
    column_data = requests.get(base_url.format('boards') + '/' + board_id + '/lists', params=auth_params).json()  
  
    # Среди всех колонок нужно найти задачу по имени и получить её id  
    task_id = None  
    for column in column_data:  
        column_tasks = requests.get(base_url.format('lists') + '/' + column['id'] + '/cards', params=auth_params).json()  
        for task in column_tasks:  
            if task['name'] == name:  
                task_id = task['id']  
                break  
        if task_id:  
            break  
  
    # Теперь, когда у нас есть id задачи, которую мы хотим переместить,  
    # Получим ID колонки, в которую мы будем перемещать задачу  column_id = column_check(column_name)  
    if column_id is None:  
        column_id = create_column(column_name)['id']  
    # И совершим перемещение:  
    requests.put(base_url.format('cards') + '/' + task_id + '/idList', data={'value': column_id, **auth_params})


Задача №3

  def read():
    column_data = requests.get(base_url.format('boards') + '/' + board_id + '/lists', params=auth_params).json()  
  
    
    for column in column_data:
        task_data = requests.get(base_url.format('lists') + '/' + column['id'] + '/cards', params=auth_params).json()  
        print(column['name'] + " - ({})".format(len(task_data)))  
  
        if not task_data:  
            print('\t' + 'Нет задач!')  
            continue  
        for task in task_data: 
            print('\t' + task['name'] + '\t' + task['id'])

    def get_task_duplicates(task_name):  
        # Получим данные всех колонок на доске  
        column_data = requests.get(base_url.format('boards') + '/' + board_id + '/lists', params=auth_params).json()  

        # Заведём список колонок с дублирующимися именами  
        duplicate_tasks = []  
        for column in column_data:  
            column_tasks = requests.get(base_url.format('lists') + '/' + column['id'] + '/cards', params=auth_params).json()  
            for task in column_tasks:  
                if task['name'] == task_name:  
                    duplicate_tasks.append(task)  
        return duplicate_tasks
        
        def move(name, column_name):  
    # Получим данные всех колонок на доске  
    column_data = requests.get(base_url.format('boards') + '/' + board_id + '/lists', params=auth_params).json()  
  
    # Среди всех колонок нужно найти задачу по имени и получить её id  
    task_id = None  
    for column in column_data:  
        column_tasks = requests.get(base_url.format('lists') + '/' + column['id'] + '/cards', params=auth_params).json()  
        for task in column_tasks:  
            if task['name'] == name:  
                task_id = task['id']  
                break  
        if task_id:  
            break  
            
  duplicate_tasks = get_task_duplicates(name)  
    if len(duplicate_tasks) > 1:  
        print("Задач с таким названием несколько штук:")  
        for index, task in enumerate(duplicate_tasks):  
            task_column_name = requests.get(base_url.format('lists') + '/' + task['idList'], params=auth_params).json()['name']  
            print("Задача №{}\tid: {}\tНаходится в колонке: {}\t ".format(index, task['id'], task_column_name))  
        task_id = input("Пожалуйста, введите ID задачи, которую нужно переместить: ")  
    else:  
        task_id = duplicate_tasks[0]['id']
        
    # Получим ID колонки, в которую мы будем перемещать задачу  column_id = column_check(column_name)  
    if column_id is None:  
        column_id = create_column(column_name)['id']  
    # И совершим перемещение:  
    requests.put(base_url.format('cards') + '/' + task_id + '/idList', data={'value': column_id, **auth_params})
