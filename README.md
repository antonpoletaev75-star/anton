import socket

HOST = "127.0.0.1"
PORT = 5000

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind((HOST, PORT))
server.listen(1)

print(f"Сервер запущен: {HOST}:{PORT}")

conn, addr = server.accept()
print(f"Подключился клиент: {addr}")

while True:
    data = conn.recv(1024)

    if not data:
        break

    message = data.decode("utf-8")

    if message == "exit":
        print("Клиент завершил работу")
        break

    print(f"Получено: {message}")
    conn.sendall(data)

conn.close()
server.close()
print("Сервер остановлен")
