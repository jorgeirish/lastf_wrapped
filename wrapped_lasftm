%pip install pylast
import pylast

apikey = "YOUR_LASTFM_API_KEY"
apisecret = "YOUR_LASTFM_API_SECRET"

# Configuración de Last.fm
API_KEY = apikey
API_SECRET = apisecret
PERIODOS_VALIDOS = ["overall", "7day", "1month", "3month", "6month", "12month"]

# Obtener información del usuario
usuario = input("Escribe tu nombre de usuario: ")
pss = pylast.md5(input("Escribe tu contraseña: "))
print(f"Periodos válidos: {', '.join(PERIODOS_VALIDOS)}")
tiempo = input("Elige un periodo de tiempo: ")

# Validar el período seleccionado
if tiempo not in PERIODOS_VALIDOS:
    print("Período de tiempo no válido. Usa uno de los siguientes:", ", ".join(PERIODOS_VALIDOS))
    exit()

# Conectar a la red de Last.fm
try:
    network = pylast.LastFMNetwork(api_key=API_KEY, api_secret=API_SECRET, username=usuario, password_hash=pss)
    user = network.get_user(usuario)
except pylast.WSError as e:
    print("Error al conectar con Last.fm:", e)
    exit()

# Obtener y mostrar el top de álbumes, canciones y artistas
try:
    # Top Álbumes
    print("\nTop Álbumes:")
    albums = user.get_top_albums(limit=5, period=tiempo)
    for album in albums:
        cover_image = album.item.get_cover_image()
        print(f"Álbum: {album.item.title}, Reproducciones: {album.weight}, Portada: {cover_image}")


    # Top Canciones
    print("\nTop Canciones:")
    tracks = user.get_top_tracks(limit=5, period=tiempo)
    for track in tracks:
        print(f"Track: {track.item.title}, Reproducciones: {track.weight}, Artista: {track.item.artist}")

    # Top Artistas
    print("\nTop Artistas:")
    artists = user.get_top_artists(limit=5, period=tiempo)
    for artist in artists:
        print(f"Artista: {artist.item.name}, Reproducciones: {artist.weight}")

    # Total Reproducciones en el periodo
    #playcount = user.get_playcount()
    #print(f"Total de reproducciones de siempre: {playcount}")

except pylast.WSError as e:
    print("Error al obtener datos:", e)
