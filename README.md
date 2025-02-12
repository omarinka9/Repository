import pandas as pd

def load_data(file_path):
    """Загрузка данных из CSV файла."""
    try:
        df = pd.read_csv(file_path)
    except FileNotFoundError:
        print(f"Файл {file_path} не найден.")
        return None
    
    return df

def filter_data(df, column_name, value):
    """Фильтрация данных по значению в указанном столбце."""
    if not isinstance(column_name, str):
        raise TypeError("Имя столбца должно быть строкой.")
    
    filtered_df = df.query(f"{column_name} == @value")
    return filtered_df

def save_filtered_data(filtered_df, output_file_path):
    """Сохранение отфильтрованных данных в новый CSV файл."""
    try:
        filtered_df.to_csv(output_file_path, index=False)
    except OSError as e:
        print(f"Произошла ошибка при сохранении файла: {e}")

if __name__ == "__main__":
    # Пример использования функций
    file_path = "data.csv"
    df = load_data(file_path)
    
    if df is not None:
        column_name = "age"
        value = 30
        
        filtered_df = filter_data(df, column_name, value)
        output_file_path = "filtered_data.csv"
        save_filtered_data(filtered_df, output_file_path)# Repository
