# 3-level-Game-Python-
Created in introduction to programming class


import random
import arcade
import math
from game_items import *



class MyApplication(arcade.Window):
    def __init__(self, width, height):
        super().__init__(width, height)

        self.instructions1 = arcade.load_texture("level 1 instructions(C).png")
        self.instructions2 = arcade.load_texture("level 2 instructions.png")
        self.instructions3 = arcade.load_texture("level 3 instructions.png")
        self.all_sprites_list = None
        self.star_list = None
        self.alien_list = None
        self.pill_list = None
        self.bullet_list = None
        self.asteroid_list = None
        self.frame_count = 0
        self.level = 4
        self.game_over = False
        self.game_over_message = "Game over."
        self.lives = 3
        # Class assets.
        self.star_sound = arcade.load_sound("coin1.ogg")
        self.explosion3_sound = arcade.load_sound("explosion3.ogg")
        self.upgrade_sound = arcade.load_sound("upgrade1.ogg")
        self.destroy_sound = arcade.load_sound("hit5.ogg")
        self.explosion4_sound = arcade.load_sound("explosion4.ogg")
        self.explosion2_sound = arcade.load_sound("explosion2.ogg")
        self.explosion_sound = arcade.load_sound("explosion1.ogg")
        self.injured_sound = arcade.load_sound("hurt1.ogg")
        # Kenney
        self.gun_sound = arcade.load_sound("laser4.mp3")

        self.score = 0
        self.player_sprite = None


    def setup1(self):
        # https://www.google.com/search?q=space+background&espv=2&site=webhp&source=lnms&tbm=isch&sa
        # =X&sqi=2&ved=0ahUKEwjn49ncwb3TAhULyoMKHQXIBm4Q_AUIBigB&biw=1536&bih=760#imgrc=2F8TImagmbM1bM:
        self.background = arcade.load_texture("469181920.jpg")

        # Sprite lists
        self.all_sprites_list = arcade.SpriteList()
        self.alien_list = arcade.SpriteList()
        self.bullet_list = arcade.SpriteList()
        self.total_time = 30.0
        self.game_over_message = "Game over."
        self.game_over = False
        self.lives = 3
        # Kenney
        self.gun_sound = arcade.load_sound("laser4.mp3")
        self.explosion_sound = arcade.load_sound("explosion1.ogg")

        # Set up the player
        self.score = 0
        # Kenney
        self.player_sprite = arcade.Sprite("spaceShips_007.png",
                                           SPRITE_SCALING)
        self.player_sprite.center_x = 50
        self.player_sprite.center_y = 70
        self.all_sprites_list.append(self.player_sprite)

        for i in range(50):
            # Kenney
            alien = arcade.Sprite("shipGreen_manned.png", SPRITE_SCALING)

            alien.center_x = random.randrange(SCREEN_WIDTH)
            alien.center_y = random.randrange(120, SCREEN_HEIGHT)

            self.all_sprites_list.append(alien)
            self.alien_list.append(alien)


    def setup2(self):
        # Background from https://www.google.com/search?q=space+background&espv=2&source=lnms&tbm=isch&sa=X&ved=
        # 0ahUKEwjbrsG-267TAhXj1IMKHUOmBtAQ_AUIBigB&biw=1536&bih=760#imgrc=p0HEptd9WFPtyM:
        self.background = arcade.load_texture("6946579-space-stars-background.jpg")
        # Sprite lists

        self.all_sprites_list = arcade.SpriteList()
        self.star_list = arcade.SpriteList()
        self.alien_list = arcade.SpriteList()
        self.pill_list = arcade.SpriteList()

        # Sets up player
        # Kenney
        self.player_sprite = arcade.Sprite("spaceShips_007.png", SPRITE_SCALING)
        self.player_sprite.center_x = 50
        self.player_sprite.center_y = 50
        self.all_sprites_list.append(self.player_sprite)

        for i in range(5):
            # Class assets
            pill = Pill("pill_yellow.png", SPRITE_SCALING * 2)

            # Positions the pill.
            pill.center_x = random.randrange(SCREEN_WIDTH)
            pill.center_y = random.randrange(SCREEN_HEIGHT)

            pill.change_y = random.randrange(1, 5)

            self.all_sprites_list.append(pill)
            self.pill_list.append(pill)

        for i in range(40):
            # Kenney
            star = Star2("laserBeige_burst.png", SPRITE_SCALING / 2)

            # Positions the star.
            star.center_x = random.randrange(SCREEN_WIDTH)
            star.center_y = random.randrange(SCREEN_HEIGHT)

            star.change_y = random.randrange(1, 8)

            self.all_sprites_list.append(star)
            self.star_list.append(star)

        for i in range(20):
            # Kenney
            alien = Alien2("shipGreen_manned.png", SPRITE_SCALING)

            # Positions the alien.
            alien.center_x = random.randrange(SCREEN_WIDTH)
            alien.center_y = random.randrange(SCREEN_HEIGHT)
            alien.change_y = random.randrange(1, 8)

            self.all_sprites_list.append(alien)
            self.alien_list.append(alien)

        self.set_mouse_visible(False)


    def setup3(self):
        # https://www.google.com/search?q=space+background&espv=2&site=webhp&source=lnms&tbm=isch&sa=X&sqi=2&ved=
        # 0ahUKEwjn49ncwb3TAhULyoMKHQXIBm4Q_AUIBigB&biw=1536&bih=760#imgrc=EaT1Nc-naAJCNM:
        self.background = arcade.load_texture("blue_space_background__looks_the_same_as_the_rest__by_darkdissolution-d7pgwmn.png")

        self.all_sprites_list = arcade.SpriteList()
        self.star_list = arcade.SpriteList()
        self.alien_list = arcade.SpriteList()
        self.pill_list = arcade.SpriteList()
        self.bullet_list = arcade.SpriteList()
        self.asteroid_list = arcade.SpriteList()

        self.score = 0
        # Kenney
        self.player_sprite = arcade.Sprite("spaceShips_007.png", SPRITE_SCALING / 2)
        self.player_sprite.center_x = 50
        self.player_sprite.center_y = 70
        self.all_sprites_list.append(self.player_sprite)

        for i in range(5):
            # Class assets
            asteroid = Asteroid("meteorBrown_big4.png", SPRITE_SCALING * 2)
            # Positions the star.

            asteroid.center_x = random.randrange(SCREEN_WIDTH)
            asteroid.center_y = random.randrange(SCREEN_HEIGHT)

            asteroid.change_y = random.randrange(1, 8)

            self.all_sprites_list.append(asteroid)
            self.asteroid_list.append(asteroid)

        for i in range(10):
            # Class assets
            pill = Pill("pill_yellow.png", SPRITE_SCALING * 2)

            # Positions the star.
            pill.center_x = random.randrange(SCREEN_WIDTH)
            pill.center_y = random.randrange(SCREEN_HEIGHT)

            pill.change_y = random.randrange(1, 5)

            self.all_sprites_list.append(pill)
            self.pill_list.append(pill)

        for i in range(50):
            # Kenney
            star = Star3("laserBeige_burst.png", SPRITE_SCALING / 2)

            # Position the center of the circle the star will orbit
            star.circle_center_x = random.randrange(SCREEN_WIDTH)
            star.circle_center_y = random.randrange(SCREEN_HEIGHT)

            # Random radius from 10 to 200
            star.radius = random.randrange(10, 200)

            # Random start angle from 0 to 2pi
            star.angle = random.random() * 2 * math.pi

            self.all_sprites_list.append(star)
            self.star_list.append(star)

        # Don't show the mouse cursor
        self.set_mouse_visible(False)


    def on_draw(self):
        arcade.start_render()
        if self.level == 4:
            arcade.draw_texture_rectangle(SCREEN_WIDTH // 2, SCREEN_HEIGHT // 2, SCREEN_WIDTH, SCREEN_HEIGHT,
                                          self.instructions1)
        elif self.level == 5:
            arcade.draw_texture_rectangle(SCREEN_WIDTH // 2, SCREEN_HEIGHT // 2, SCREEN_WIDTH, SCREEN_HEIGHT,
                                          self.instructions2)
        elif self.level == 6:
            arcade.draw_texture_rectangle(SCREEN_WIDTH // 2, SCREEN_HEIGHT // 2, SCREEN_WIDTH, SCREEN_HEIGHT,
                                          self.instructions3)
        else:
            arcade.draw_texture_rectangle(SCREEN_WIDTH // 2, SCREEN_HEIGHT // 2, SCREEN_WIDTH, SCREEN_HEIGHT,
                                          self.background)

            self.all_sprites_list.draw()

            input = "Score: {}".format(self.score)
            output = "Lives: " + str(self.lives)
            input1 = "You won!"
            arcade.draw_text(input, 10, 20, arcade.color.WHITE, 30)

            if self.star_list != None and len(self.star_list) > 0:
                arcade.draw_text(output, 10, 60, arcade.color.WHITE, 30)

            if self.level == 1:
                # Calculate minutes
                minutes = int(self.total_time) // 60

                # Calculate seconds by using a modulus (remainder)
                seconds = int(self.total_time) % 60

                output = "Time: {:02d}:{:02d}".format(minutes, seconds)
                arcade.draw_text(output, 10, 60, arcade.color.WHITE, 30)

            if self.game_over:
                arcade.draw_text(self.game_over_message, 400, 450, arcade.color.RED, 100)


    def on_mouse_motion(self, x, y, dx, dy):
        if not self.game_over:
            self.player_sprite.center_x = x
            self.player_sprite.center_y = y


    def on_mouse_press(self, x, y, button, modifiers):
        if self.level == 4:
            self.level = 1
        elif self.level == 5:
            self.level = 2
        elif self.level == 6:
            self.level = 3
        elif not self.game_over:
            arcade.sound.play_sound(self.gun_sound)
            # Kenney
            bullet = Bullet("spaceMissiles_003.png", SPRITE_SCALING * 1.5)

            bullet.angle = 180

            bullet.center_x = self.player_sprite.center_x
            bullet.bottom = self.player_sprite.top

            self.all_sprites_list.append(bullet)
            self.bullet_list.append(bullet)
        elif self.game_over:
            self.level = 4
            self.setup1()


    def animate2(self, delta_time):
        if len(self.star_list) > 0 and self.lives > 0:
            self.all_sprites_list.update()

        hit_list1 = arcade.check_for_collision_with_list(self.player_sprite, self.alien_list)
        for alien in hit_list1:
            self.lives -= 1
            alien.kill()
            arcade.sound.play_sound(self.explosion2_sound)

        hit_list2 = arcade.check_for_collision_with_list(self.player_sprite, self.star_list)
        for star in hit_list2:
            self.score += 1
            star.kill()
            arcade.sound.play_sound(self.star_sound)

        hit_list3 = arcade.check_for_collision_with_list(self.player_sprite, self.pill_list)
        for pill in hit_list3:
            self.lives += 1
            pill.kill()
            arcade.sound.play_sound(self.upgrade_sound)
        if self.lives <= 0:
            self.game_over = True
        if len(self.star_list) == 0:
            self.level = 6
            self.setup3()


    def animate3(self, delta_time):
        if len(self.star_list) > 0 and self.lives > 0:
            self.all_sprites_list.update()

        if self.frame_count % 150 == 0:
            for x in range(0, 1500, 65):
                # Randomly skip a box so the player can find a way through
                if random.randrange(5) > 0:
                    # Kenney
                    alien = Alien3("shipGreen_manned.png", SPRITE_SCALING)
                    alien.center_x = x
                    alien.bottom = SCREEN_HEIGHT
                    alien.change_y = random.randrange(-2, -1)
                    self.all_sprites_list.append(alien)
                    self.alien_list.append(alien)
        self.frame_count += 1

        for bullet in self.bullet_list:
            hit_list = arcade.check_for_collision_with_list(bullet, self.alien_list)
            if len(hit_list) > 0:
                bullet.kill()
            for alien in hit_list:
                alien.kill()
                arcade.sound.play_sound(self.explosion3_sound)

            hit_list0 = arcade.check_for_collision_with_list(bullet, self.asteroid_list)
            for asteroid in hit_list0:
                asteroid.kill()
                arcade.sound.play_sound(self.explosion4_sound)
            if bullet.bottom > SCREEN_HEIGHT:
                bullet.kill()

        hit_list2 = arcade.check_for_collision_with_list(self.player_sprite, self.star_list)
        for star in hit_list2:
            star.kill()
            self.score += 1
            arcade.sound.play_sound(self.star_sound)

        hit_list1 = arcade.check_for_collision_with_list(self.player_sprite, self.alien_list)
        for alien in hit_list1:
            self.lives -= 1
            alien.kill()
            arcade.sound.play_sound(self.injured_sound)

        hit_list3 = arcade.check_for_collision_with_list(self.player_sprite, self.pill_list)
        for pill in hit_list3:
            self.lives += 1
            pill.kill()
            arcade.sound.play_sound(self.upgrade_sound)

        hit_list4 = arcade.check_for_collision_with_list(self.player_sprite, self.asteroid_list)
        for asteroid in hit_list4:
            self.lives -= 1
            asteroid.kill()
            arcade.sound.play_sound(self.destroy_sound)
        if self.lives <= 0:
            self.game_over = True
        if len(self.star_list) == 0:
            self.game_over = True
            self.game_over_message = "You won!"


    def animate1(self, delta_time):
        if len(self.alien_list) > 0 and self.total_time > 0:
            self.all_sprites_list.update()

        for bullet in self.bullet_list:
            hit_list = arcade.check_for_collision_with_list(bullet, self.alien_list)
            if len(hit_list) > 0:
                bullet.kill()

            for alien in hit_list:
                alien.kill()
                self.score += 1
                arcade.sound.play_sound(self.explosion_sound)

            if bullet.bottom > SCREEN_HEIGHT:
                bullet.kill()

        self.total_time -= delta_time
        if self.total_time < 0:
            self.total_time = 0
            self.game_over = True
        if len(self.alien_list) == 0:
            self.total_time = 0
            self.level = 5
            self.setup2()


    def animate(self, delta_time):
        if self.level == 3:
            self.animate3(delta_time)
        if self.level == 2:
            self.animate2(delta_time)
        if self.level == 1:
            self.animate1(delta_time)



window = MyApplication(SCREEN_WIDTH, SCREEN_HEIGHT)
window.setup1()
arcade.run()
