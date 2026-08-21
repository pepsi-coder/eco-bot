import discord

# La variable intents almacena los privilegios del bot
intents = discord.Intents.default()
# Activar el privilegio de lectura de mensajes
intents.message_content = True
# Crear un bot en la variable cliente y transferirle los privilegios
client = discord.Client(intents=intents)

@client.event
async def on_ready():
    print(f'Hemos iniciado sesión como {client.user}')

@client.event
async def on_message(message):
    if message.author == client.user:
        return
    if message.content.startswith('$hello'):
        await message.channel.send("Haiiii :3")
    elif message.content.startswith('$bye'):
        await message.channel.send("bai baaaaa\U0001f642")
    elif message.content.startswith('$recycle'):
        trash_type = message.content[len('$recycle'):].strip().lower()
        bins = { 
            'paper': 'dry trash',
            'carton': 'dry trash',
            'eaten fruit': 'wet/organic trash',
            'bottle': 'recycle',
            'can': 'recycle'
        }

        if trash_type in bins:
            await message.channel.send(f'{trash_type} goes in the {bins[trash_type]} bro :>')
        else:
            await message.channel.send(
                'Use `$recycle` followed by one of these options: '
                'paper, carton, eaten fruit, bottle, or can.'
            )
    elif message.content.startswith('$ecohelp'):
            await message.channel.send("Hello, i will brind you help with how to not contamine the environment, and how to take care of it. \n\n"
                                       "1. Reduce, Reuse, Recycle: Reduce waste by using less, reuse items when possible, and recycle materials to conserve resources.\n"
                                       "2. Conserve Energy: Turn off lights and electronics when not in use, use energy-efficient appliances, and consider renewable energy sources.\n"
                                       "3. Use Eco-Friendly Products: Choose products made from sustainable materials, avoid single-use plastics, and opt for environmentally friendly cleaning products.\n"
                                       "4. Plant Trees and Support Green Spaces: Trees absorb carbon dioxide and provide oxygen. Support local parks and green initiatives.\n"
                                       "5. Educate Yourself and Others: Stay informed about environmental issues and share knowledge with friends and family to promote eco-conscious behavior.")
    elif message.content.startswith('$trashbinhelp'):
            await message.channel.send("There are several types of trash bins: dry trash, wet/organic trash, and recyclables. Use $recycle followed by the type of trash to know which bin it goes in.")
client.run("")
