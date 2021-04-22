CREATE TABLE public.album_singer
(
    id_album integer NOT NULL,
    id_singer integer NOT NULL,
    CONSTRAINT pk_albums_singer PRIMARY KEY (id_album, id_singer),
    CONSTRAINT album_singer_id_album_fkey FOREIGN KEY (id_album)
        REFERENCES public.albums (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION,
    CONSTRAINT album_singer_id_singer_fkey FOREIGN KEY (id_singer)
        REFERENCES public.singer (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

TABLESPACE pg_default;

ALTER TABLE public.album_singer
    OWNER to admin;
    
    CREATE TABLE public.albums
(
    id integer NOT NULL DEFAULT nextval('albums_id_seq'::regclass),
    name character varying(60) COLLATE pg_catalog."default" NOT NULL,
    years integer NOT NULL,
    CONSTRAINT albums_pkey PRIMARY KEY (id)
)

TABLESPACE pg_default;

ALTER TABLE public.albums
    OWNER to admin;
    
    
    CREATE TABLE public.collection
(
    id integer NOT NULL DEFAULT nextval('collection_id_seq'::regclass),
    name character varying(60) COLLATE pg_catalog."default" NOT NULL,
    years integer NOT NULL,
    CONSTRAINT collection_pkey PRIMARY KEY (id)
)

TABLESPACE pg_default;

ALTER TABLE public.collection
    OWNER to admin;
    
    (
    id_collection integer NOT NULL,
    id_track integer NOT NULL,
    CONSTRAINT pk_collection_track PRIMARY KEY (id_collection, id_track),
    CONSTRAINT collection_tracks_id_collection_fkey FOREIGN KEY (id_collection)
        REFERENCES public.collection (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION,
    CONSTRAINT collection_tracks_id_track_fkey FOREIGN KEY (id_track)
        REFERENCES public.track (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

TABLESPACE pg_default;

ALTER TABLE public.collection_tracks
    OWNER to admin;
    
    
    CREATE TABLE public.genre
(
    id integer NOT NULL DEFAULT nextval('genre_id_seq'::regclass),
    name character varying(60) COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT genre_pkey PRIMARY KEY (id)
)

TABLESPACE pg_default;

ALTER TABLE public.genre
    OWNER to admin;
    
    CREATE TABLE public.genre_singer
(
    id_genre integer NOT NULL,
    id_singer integer NOT NULL,
    CONSTRAINT pk_genre_singer PRIMARY KEY (id_genre, id_singer),
    CONSTRAINT genre_singer_id_genre_fkey FOREIGN KEY (id_genre)
        REFERENCES public.genre (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION,
    CONSTRAINT genre_singer_id_singer_fkey FOREIGN KEY (id_singer)
        REFERENCES public.singer (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

TABLESPACE pg_default;

ALTER TABLE public.genre_singer
    OWNER to admin;
    
    
    CREATE TABLE public.singer
(
    id integer NOT NULL DEFAULT nextval('singer_id_seq'::regclass),
    singer character varying(60) COLLATE pg_catalog."default" NOT NULL,
    alias character varying(60) COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT singer_pkey PRIMARY KEY (id),
    CONSTRAINT singer_singer_key UNIQUE (singer)
)

TABLESPACE pg_default;

ALTER TABLE public.singer
    OWNER to admin;
    
    
    CREATE TABLE public.track
(
    id integer NOT NULL DEFAULT nextval('track_id_seq'::regclass),
    name character varying(60) COLLATE pg_catalog."default" NOT NULL,
    duration integer NOT NULL,
    id_album integer,
    CONSTRAINT track_pkey PRIMARY KEY (id),
    CONSTRAINT track_id_album_fkey FOREIGN KEY (id_album)
        REFERENCES public.albums (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

TABLESPACE pg_default;

ALTER TABLE public.track
    OWNER to admin;
